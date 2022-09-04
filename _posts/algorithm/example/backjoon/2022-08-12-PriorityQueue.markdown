---
layout: posts
title:  "Priority Queue"
date:   2022-08-11 12:10:28 +0900
categories: datastructure
tags:
  - python
  - priority queue
  - heap
---

# Introduction

# Example

https://www.acmicpc.net/step/13

## 최대 힙

{% highlight python %}
import sys
import heapq
input = sys.stdin.readline

N = int(input())

q = []
for _ in range(N):
    x = int(input())
    if x > 0 :
        heapq.heappush(q,-x)
    else:
        if len(q) > 0:
            print(-heapq.heappop(q))
        else:
            print(0)
{% endhighlight %}

## 최소 힙

{% highlight python %}
import sys
import heapq
input = sys.stdin.readline

N = int(input())

q = []
for _ in range(N):
    x = int(input())
    if x > 0 :
        heapq.heappush(q,x)
    else:
        if len(q) > 0:
            print(heapq.heappop(q))
        else:
            print(0)
{% endhighlight %}

## 절댓값 힙

{% highlight python %}
import sys
import heapq
input = sys.stdin.readline

N = int(input())

q = []
for _ in range(N):
    x = int(input())
    if x > 0 :
        heapq.heappush(q,(abs(x),x))
    elif x < 0 :
        heapq.heappush(q,(abs(x),x))
    else:
        if len(q) > 0:
            x, sig= heapq.heappop(q)
            print(sig)
        else:
            print(0)
{% endhighlight %}

## 가운데를 말해요

전체 값을 반으로 나누어 두 개의 힙에 저장하여 구현하였다.
무슨 이유인지 값이 틀렸다고 나온다.

{% highlight python %}
import sys
import heapq
input = sys.stdin.readline

N = int(input())

q_high = []
q_low = []

first = int(input())

second = int(input())
if first > second:
    heapq.heappush(q_high,(first,first))
    heapq.heappush(q_low,(-second,second))
else:
    heapq.heappush(q_high,(second,second))
    heapq.heappush(q_low,(-first,first))

for _ in range(N-2):
    next = int(input())
    if len(q_high) == len(q_low):
        if q_low[0][1] < next and q_high[0][1] < next:
            p, val = heapq.heappop(q_high)
            heapq.heappush(q_low,(-p,val))
            heapq.heappush(q_high,(next,next))
        else:
            heapq.heappush(q_low,(-next,next))
    else:
        if q_low[0][1] > next:
            p, val = heapq.heappop(q_low)
            heapq.heappush(q_high,(-p,val))
            heapq.heappush(q_low,(-next,next))
        else:
            heapq.heappush(q_high,(next,next))
    print(q_low[0][1])
{% endhighlight %}

접근 방법은 맞았으나, 조건문 처리에서 틀렸다.
조건문 처리를 잘 하는 방법을 찾는 것이 필요해보인다.

{% highlight python %}
import sys
import heapq
input = sys.stdin.readline

N = int(input())

q_high = []
q_low = []

for _ in range(N):
    next = int(input())
    if len(q_high) == len(q_low):
        heapq.heappush(q_low,(-next,next))
    else:
        heapq.heappush(q_high,(next,next))
    if q_high and q_low[0][1] > q_high[0][1]:
        pLow, vLow = heapq.heappop(q_low)
        pHigh, vHigh = heapq.heappop(q_high)
        heapq.heappush(q_high,(-pLow,vLow))
        heapq.heappush(q_low,(-pHigh,vHigh))
    print(q_low[0][1])
{% endhighlight %}