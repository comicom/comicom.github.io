---
layout: posts
title:  "Backjoon Algorithm 1-1: Summary"
date:   2022-08-27 17:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
---

# Introduction

## Data Structure 1

* 스택, 큐

linked list로 구현

* 데크

{% highlight python %}
from collections import deque

d = deque()
d.appendleft()
d.append()
d.popleft()
d.pop()
{% endhighlight %}

## Math 1

* 최대공약수

2개의 자연수 a, b(a>b)에 대해서 a를 b로 나눈 나머지가 r일 때, a와 b의 최대공약수는 b와 r의 최대공약수와 같다.

{% highlight python %}
a = 24
b = 18

r = a%b
while r != 0:
  big = b
  small = r
  r = big%small
print(small)
>> 6
{% endhighlight %}

* 최소공배수

큰값\*작은값\*최대공약수

* 소수

{% highlight python %}
import math

# 소수 판별 함수(에라토스테네스의 체)
def is_prime_number(n):
    # 2부터 n까지의 모든 수에 대하여 소수 판별
    array = [True for i in range(n+1)] # 처음엔 모든 수가 소수(True)인 것으로 초기화(0과 1은 제외)

    # 에라토스테네스의 체
    for i in range(2, int(math.sqrt(n)) + 1): #2부터 n의 제곱근까지의 모든 수를 확인하며
        if array[i] == True: # i가 소수인 경우(남은 수인 경우)
            # i를 제외한 i의 모든 배수를 지우기
            j = 2
            while i * j <= n:
                array[i * j] = False
                j += 1

    return [ i for i in range(2, n+1) if array[i] ]
{% endhighlight %}

## Dynamic Programming 1

점화식 구하는 것이 관건