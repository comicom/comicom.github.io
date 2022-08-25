---
layout: posts
title:  "How to Reduce Docekr Image Size"
date:   2022-07-08 12:10:28 +0900
categories: docker
tags:
  - docker
  - dockerfile
---

## 가벼운 Base image를 사용

이미지에는 불필요한 것들이 많이 포함되어 있을수 있기때문에 debian계열로는 slim, jessie, alpine등을 사용하여 용량을 줄일 수 있음
단, 필요한 패키지, 파일이 있을수 있음

## Dockerfile 명령을 체인으로 사용
Dockerfile에서 RUN명령을 개별로 실행시 실행이 끝날때마다 중간 이미지가 생성
체인으로 명령을 실행하면 한개만 만들어지기 때문에 크기가 줄어듬

개별 실행 예제

{% highlight %}
RUN wget -nv
RUN tar -xvf someutility-v1.0.0.tar.gz
RUN mv /tmp/someutility-v1.0.0/someutil /usr/bin/someutil
{% endhighlight %}

체인 실행 예제

{% highlight %}
RUN wget -nv \
tar -xvf someutility-v1.0.0.tar.gz \
mv /tmp/someutility-v1.0.0/someutil /usr/bin/someutil
{% endhighlight %}

## 패키지 관리자를 정리

apt-get을 실행 했다면, apt-get clean을 넣어주고, --no-install-recommends옵션(최소 설치)을 넣는다.
/var/cache/apt/archives 디렉토리에 있는 다운로드 파일을 지워줌
/var/lib/pat/lists 디렉토리를 지워 패키지 리스트 파일도 지워줌

{% highlight %}
RUN apt-get update && apt-get install -y \
    aufs-tools \
    automake \
    build-essential \
    curl \
    dpkg-sig \
    libcap-dev \
    libsqlite3-dev \
    mercurial \
    reprepro \
    ruby1.9.1 \
    ruby1.9.1-dev \
    s3cmd=1.1.* \
 && rm -rf /var/lib/apt/lists/*
{% endhighlight %}

## 불필요한 파일 정리

curl을 통한 파일다운로드시 필요한 파일을 설치한 후 삭제
시점은 Docker명령어에수 수행해야하며 체인을 사용해야지만 최종이미지에 포함되지 않는다.
만약 개별로 수행시 각 RUN마다 레이어가 생겨서 file.zip이 포함된다.

{% highlight %}
RUN curl http://xx.xxx.com/file.zip \
RUN tar xvzf file.zip \
RUN rm file.zip
{% endhighlight %}

## docker image에서 불필요한 Layer가 있는지 확인

--no-trunc: 명령어, 설명을 ...으로 표시하지 않고 전체를 보여준다.
각 layer마다 사용된 용량이 표시된다.

{% highlight %}
docker history gcr.io/kfserving/pytorchserver:0.3.0 --no-trunc
{% endhighlight %}
{% highlight %}
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
2e560760b2db        6 months ago        /bin/sh -c #(nop) ENTRYPOINT &{["/run.sh"]}     0 B                 
<missing>           6 months ago        /bin/sh -c #(nop) COPY file:6d7449b1aeffb25aa   1.602 kB            
<missing>           6 months ago        /bin/sh -c #(nop) EXPOSE 3000/tcp               0 B                 
<missing>           6 months ago        /bin/sh -c #(nop) VOLUME [/var/lib/grafana /v   0 B                 
<missing>           6 months ago        |1 GRAFANA_VERSION=3.1.1-1470047149 /bin/sh -   137.7 MB            
<missing>           6 months ago        /bin/sh -c #(nop) ARG GRAFANA_VERSION           0 B                 
<missing>           11 months ago       /bin/sh -c #(nop) CMD ["/bin/bash"]             0 B                 
<missing>           11 months ago       /bin/sh -c #(nop) ADD file:b5391cb13172fb513d   125.1 MB
{% endhighlight %}

## 상황에 맞게 ADD 명령어 사용
ADD, COPY는 기능을 포함하면서도, HTTP로 파일을 다운로드하거나, tar/zip파일을 풀어 설치하는 기능을 가지고 있음.
하지만, curl, wget을 사용하는 것이 좋다.
이유 : ADD를 통해 압축파일을 다운받고, 압축파일을 지워야 하는데 체인으로 처리 할수 없다.

{% highlight %}
ADD http://xx.xxx.com/file.tar.gz
RUN tar zvxf file.tar.gz
RUN rm file.tar.gz
{% endhighlight %}

ADD대신 RUN을 사용

{% highlight %}
RUN wget http://xx.xxx.com/file.zip \
    tar xvzf filr.tar.gz \
    rm file.tar.gz
{% endhighlight %}

ADD를 상용하기에 적합한 케이스

로컬 압축파일을 압축을 해제할때,
{% highlight %}
ADD file.tar.gz ./
{% endhighlight %}

만약 copy와 run을 사용하게 되면, 불필요한 layer를 생성하게 된다.
{% highlight %}
COPY file.tar.gz ./
RUN tar xvzf file.tar.gz
{% endhighlight %}

## 멀티-스테이지 빌드

Dockerfile 1개에 FROM 구문을 여러 개 두는 방식
각 FROM 명령문을 기준으로 스테이지를 구분하여, 특정 스테이지에서 생성된 것중에 사용되지 않거나 불필요한 모든 것을 무시하고, 필요한 부분만 가져와서 새로운 베이스 이미지로 빌드하여 생성

Pipfile에는 uwgi라는 패키지의 의존성을 명시하고 있고, 이 패키지를 위해서는 gcc가 필요하기때문에 apt-get install gcc를 실행 해야함
여기서, gcc는 uwgi설치에만 관여하고, 실제 애플리케이션 실행환경에는 필요 하지 않기때문에 멀티-스테이지 빌드를 사용할 수 있음

{% highlight %}
COPY --from=builder: 전 단계 스테이지 빌드에서 생성된 특정 결과물만 새로운 BASE이미지로 복사해서 이미지를 생성
FROM python:3.8-slim-buster AS builder

RUN apt-get update && apt-get install -y gcc

WORKDIR /tmp
RUN pip install pipenv

COPY Pipfile /tmp/Pipfile
COPY Pipfile.lock /tmp/Pipfile.lock

RUN pipenv install --system --deploy

FROM python:3.8-slim-buster
COPY --from=builder /usr/local/lib/python3.8/site-packages /usr/local/lib/python3.8/site-packages

CMD ["pip", "freeze"]
{% endhighlight %}

## .dockerignore 활용하기
docker build시 명령어 COPY등을 통해서 프로젝트 파일을 컨테이너로 복사할 때 폭더, 파일등을 배제 하는 역할