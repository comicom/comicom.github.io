---
layout: posts
title:  "Backjoon Algorithm 1-1: Data structure"
date:   2022-08-25 23:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - data structure
---

# Introduction

## 리스트

아래는 리스트의 기본 개념에 대해 정리한 것이다.

{% highlight python %}
lists = []

# 맨 뒤에 값 추가
lists.append(x)
# a 위치에 b 값 추가
lists.insert(a,b)
# 리스트에서 특정 값 제거
# x가 리스트에 여러개 있으면 맨 처음 x삭제
# x가 리스트에 존재하지 않느다면 에러 발생
lists.remove(x)
# 인덱스 값 반환 후 삭체
lists.pop()
lists.pop(0)
# 리스트 연결
lists.extend(lists2)

# 리스트 복사
lists.copy()
# 리스트 뒤집기
lists.revers()
# 리스트 정렬
lists.sort()
# 리스트 값 x의 개수 세기
lists.count(x)
# 리스트 값 x의 위치 반환
lists.index(x)
{% endhighlight %}

* 얕은 복사
  - 대입 연산자 사용
* 깊은 복사
  - copy() 함수 사용
  - 슬라이싱 사용

아래는 리스트의 활용에 대해서 설명한 것이다.

### 스택

stack은 LIFO(Last Input First Out)구조이다.
따라서 pop 할 때 append 된 항목이 출력되어야 한다. 

{% highlight python %}
lists = []
lists.append(10000)
lists.pop()
{% endhighlight %}

note.

stack module [!ref](https://runestone.academy/runestone/books/published/pythonds/BasicDS/ImplementingaStackinPython.html)

### 큐

stack은 FIFO(Firts Input First Out)구조이다.
따라서 pop 할 때 첫 번째 인덱스에 있는 값이 출력되어야 한다.

{% highlight python %}
import sys
input = sys.stdin.readline

N = int(input())
q = []
for _ in range(N):
    cmd = input().split()
    if cmd[0] == "push":
        q.append(cmd[1])
    if cmd[0] == "front":
        if len(q) != 0:
            print(q[0])
        else:
            print(-1)
    if cmd[0] == "back":
        if len(q) != 0:
            print(q[-1])
        else:
            print(-1)
    if cmd[0] == "size":
        print(len(q))
    if cmd[0] == "empty":
        if len(q) == 0:
            print(1)
        else:
            print(0)
    if cmd[0] == "pop":
        if len(q) != 0:
            print(q.pop(0))
        else:
            print(-1)
{% endhighlight %}

note.

queue module [!ref](https://docs.python.org/ko/3.7/library/queue.html)

## 집합

python 집합 자료형.
순서가 없고 중복을 허용하지 않는다는 특징을 가진다.

순서가 없기 때문에 인덱스를 이용해서 값을 참조할 수 없다.

* 기본 사용 방법

{% highlight python %}
# 집합 선언
set1 = set([1,2,3])
# 값 하나 추가 : add(x)
set1.add(4)
print(set1) 
# 값 여러개 추가 : update(x)
set1.update([5,6,7,8,9,10])
print(set1) 
# 값 제거 : remove(x)
set1.remove(10)
print(set1)
# 값 안전하게 제거 : discard(x) // 없으면 제거 안함, 속도는 remove보다 느림
set1.remove(1)
print(set1)
# 집합 set1 제거
del set1
{% endhighlight %}

* 집합 연산 (교집합, 합집합, 차집합)

{% highlight python %}
# 집합 선언
set1 = set([1,2,3])
set2 = set([2,4,5,6])
set3 = set()
# 공집합 
# set1과 set2의 교집합
print(set1 & set2)
print(set1.intersection(set2)) 
# set1과 set2의 합집합
print(set1 | set2)
print(set1.union(set2)) 
# set1과 set2의 차집합
print(set1 - set2)
print(set1.difference(set2))
print(set2.difference(set1))
# set1과 set2의 합집합에서 교집합을 뺀 차집합
print(set1 ^ set2)
{% endhighlight %}

## 우선순위 큐 (힙)

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
