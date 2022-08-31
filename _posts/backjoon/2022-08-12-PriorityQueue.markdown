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

스택은 가장 나중에 삽입된 데이터를 가장 먼저 삭제하고, 큐는 가장 먼저 삽입된 데이터를 가장 먼저 삭제한다. 우선순위 큐는 우선순위가 가장 높은 데이터를 가장 먼저 삭제한다는 점이 특징이다.

힙은 특정한 규칙을 가지는 트리로, 최댓값과 최솟값을 찾는 연산을 빠르게 하기 위해 고안된 완전이진트리를 기본으로 한다.

* 최소 힙: 부모 노드의 키값이 자식 노드의 키값보다 항상 작은 힙
* 최대 힙: 부모 노드의 키값이 자식 노드의 키값보다 항상 큰 힙

파이썬에서는 우선순위 큐가 필요할 때 PriorityQueue 혹은 heapq를 사용할 수 있는데, 이 두 라이브러리는 모두 우선순위 큐 기능을 지원한다. 다만, PriorityQueue 보다는 일반적으로 heapq가 더 빠르게 동작하기 때문에 수행 시간이 제한된 상황에서는 heapq를 사용하는 것을 권장한다.

또한 우선순위 큐를 구현할 때는 내부적으로 최소 힙(Min Heap) 혹은 최대 힙(Max Heap)을 이용한다. 최소 힙을 이용하는 경우 '값이 낮은 데이터가 먼저 삭제'되며, 최대 힙을 이용하는 경우 '값이 큰 데이터가 먼저 삭제'된다. 파이썬 라이브러리에서는 기본적으로 최소 힙 구조를 이용하는데 다익스트라 최단 경로 알고리즘에서는 비용이 적은 노드를 우선하여 방문하므로 최소 힙 구조를 기반으로 하는 파이썬의 우선순위 큐 라이브러리를 그대로 사용하면 적합하다.

또한 최소 힙을 최대 힙처럼 사용하기 위해서 일부러 우선순위에 해당하는 값에 음수 부호(-)를 붙여서 넣었다가, 나중에 우선순위 큐에서 꺼낸 다음에 다시 음수 부호(-)를 붙여서 원래의 값으로 돌리는 방식을 사용할 수 있다. 이러한 테크닉도 실제 코딩 테스트 환경에서는 자주 사용되기 때문에 기억해 놓아야 한다.

{% highlight python %}
import heapq

heapq.heappush(q, (0, start))
heapq.heappop(q)
heapq.heapify(x)             # 리스트 x를 즉각적으로 heap으로 변환함
{% endhighlight %}

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