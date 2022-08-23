---
layout: posts
title:  "코드업 Python 100제"
date:   2022-08-23 12:10:28 +0900
categories: algorithm
tags:
  - python
  - algorithm
---

# Introduction

## [기초-종합] 빛 섞어 색 만들기(설명)(py)

빨녹파(r, g, b) 각 빛의 가짓수가 공백을 두고 입력된다.
예를 들어, 3 3 3 은 빨녹파 빛에 대해서 각각 0~2까지 3가지 색이 있음을 의미한다.
0 <= r,g,b <= 127

만들 수 있는 rgb 색의 정보를 오름차순(계단을 올라가는 순, 12345... abcde..., 가나다라마...)으로
줄을 바꿔 모두 출력하고, 마지막에 그 개수를 출력한다.

{% highlight python %}
from itertools import product

r, g, b = map(int,input().split())

iter1 = range(r)
iter2 = range(g)
iter3 = range(b)

# 데카르트 곱연산
result = list(product(iter1,iter2,iter3))
for res in result:
  print("{0} {1} {2}".format(res[0], res[1], res[2]))
print(len(result))
{% endhighlight %}

## [기초-종합] 함께 문제 푸는 날

같은 날 동시에 가입한 인원 3명이 규칙적으로 방문하는,
방문 주기가 공백을 두고 입력된다. (단, 입력값은 100이하의 자연수이다.)

3명이 다시 모두 함께 방문해 문제를 풀어보는 날(동시 가입/등업 후 며칠 후?)을 출력한다.

### 간단한 방법 (부르트포스)
{% highlight python %}
a, b, c = map(int, input().split())

d = 1
while d%a!=0 or d%b!=0 or d%c!=0 :
  d += 1
print(d)
{% endhighlight %}

### 최소공배수

## [기초-리스트] 이상한 출석 번호 부르기1(py)

## [기초-리스트] 이상한 출석 번호 부르기2(py)

## [기초-리스트] 이상한 출석 번호 부르기3(py)

## [기초-리스트] 바둑판에 흰 돌 놓기(설명)(py)

## [기초-리스트] 바둑알 십자 뒤집기(py)

## [기초-리스트] 설탕과자 뽑기(py)

## [기초-리스트] 성실한 개미(py)