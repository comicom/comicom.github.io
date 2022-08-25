---
layout: posts
title:  "Download-only-one-directory"
date:   2022-08-25 17:10:28 +0900
categories: git
tags:
  - git
---

Git 명령어를 사용한 하위 디렉토리 다운로드
Clone 할 로컬 저장소 생성

{% highlight shell %}
  git init "로컬저장소명"
  cd "로컬저장소명"
{% endhighlight %}

일부 경로의 파일만 다운로드 가능하도록, sparse Checkout 을 True 로 설정

{% highlight shell %}
  git config core.sparseCheckout true
{% endhighlight %}
다운로드 할 원격 저장소 주소 설정

{% highlight shell %}
  git remote add -f origin "원격저장소주소"
{% endhighlight %}
다운로드 받길 원하는 폴더나 파일의 경로를 .git/info/sparse-checkout 파일에 기술

폴더일 경우, 자동으로 하위 폴더가 포함된다.

{% highlight shell %}
echo "파일및폴더경로" >> .git/info/sparse-checkout
{% endhighlight %}

git pull 명령어를 사용해, sparse-checkout 에 기술된 경로의 파일만 다운로드

{% highlight shell %}
  git pull origin main
{% endhighlight %}