---
layout: posts
title:  "[백준 code.plus] 500 - 브루트 포스, 수 이어 쓰기 1"
date:   2022-10-18 12:34:28 +0900
categories: BackjoonSeries:500-Bruteforce
tags:
  - python
  - algorithm
  - bruteforce
  - code.plus
  - series
---

# Introduction

https://www.acmicpc.net/problem/1748

## 문제
1부터 N까지의 수를 이어서 쓰면 다음과 같이 새로운 하나의 수를 얻을 수 있다.

1234567891011121314151617181920212223...

이렇게 만들어진 새로운 수는 몇 자리 수일까? 이 수의 자릿수를 구하는 프로그램을 작성하시오.

## 입력
첫째 줄에 N(1 ≤ N ≤ 100,000,000)이 주어진다.

## 출력
첫째 줄에 새로운 수의 자릿수를 출력한다.

# 풀이

## 설계

* N의 범위가 크고 시간제한이 있기 때문에 단순하게 범위에 따라 다르게 연산하도록 작성하였다.

## 코딩

{% highlight python %}
N = int(input())

result = 0
if N < 10:
    result = N*1
elif N < 100:
    result = 9+(N-9)*2
elif N < 1000:
    result = 9+90*2+(N-99)*3
elif N < 10000:
    result = 9+90*2+900*3+(N-999)*4
elif N < 100000:
    result = 9+90*2+900*3+9000*4+(N-9999)*5
elif N < 1000000:
    result = 9+90*2+900*3+9000*4+90000*5+(N-99999)*6
elif N < 10000000:
    result = 9+90*2+900*3+9000*4+90000*5+900000*6+(N-999999)*7
elif N < 100000000:
    result = 9+90*2+900*3+9000*4+90000*5+900000*6+9000000*7+(N-9999999)*8
elif N == 100000000:
    result = 9+90*2+900*3+9000*4+90000*5+900000*6+9000000*7+90000000*8+9
print(result)
{% endhighlight %}
