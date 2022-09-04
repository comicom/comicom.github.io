---
layout: posts
title:  "Queue / Deque"
date:   2022-09-03 05:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - queue
  - deque
---

# Introduction

큐와 덱을 구현하고 사용해 봅시다.

# Example

https://www.acmicpc.net/step/49

## 큐 2

큐의 개념을 익히고 실습하는 문제. 연산 당 시간 복잡도가 O(1)이어야 한다는 점에 유의하세요.

deque 함수를 이용하여 해결

{% highlight python %}
import sys
from collections import deque
input = sys.stdin.readline

N = int(input())
q = deque([])
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
            print(q.popleft())
        else:
            print(-1)
{% endhighlight %}

## 카드 2

큐를 사용하여 동작을 구현하는 문제

{% highlight python %}
import sys
from collections import deque
input = sys.stdin.readline

N = int(input())

q = deque(range(1,N+1))
cmd = True
while len(q) != 1:
    if cmd == True:
        q.popleft()
        cmd = False
    else:
        chg = q.popleft()
        q.append(chg)
        cmd = True
print(q[0])
{% endhighlight %}

## 요세푸스 문제 0

큐를 이용해 제거 과정을 구현하는 문제

{% highlight python %}
import sys
from collections import deque
input = sys.stdin.readline

N, K = map(int,input().split())

result = "<"
q = deque(range(1,N+1))
cnt = K-1
while q:
    if cnt == 0:
        num = q.popleft()
        result += "{}, ".format(num)
        cnt = K-1
    else:
        num = q.popleft()
        q.append(num)
        cnt -= 1
print(result[:-2]+">")
{% endhighlight %}

## 프린터 큐

큐의 개념이 응용된 문제

{% highlight python %}
import sys
from collections import deque
input = sys.stdin.readline

T = int(input())
for _ in range(T):
    N, M = map(int,input().split())
    numbers = list(map(int,input().split()))
    
    q = deque([])
    for idx in range(N):
        q.append([numbers[idx],idx])
    check_q = deque(sorted(q, key=lambda x:(-x[0],x[1])))

    find_flag = False
    cnt = 0
    while True:
        num, idx = q.popleft()
        if num == check_q[0][0]:
            cnt += 1
            if idx == M:
                break
            check_q.popleft()
        else:
            q.append([num,idx])
    print(cnt)
{% endhighlight %}

## 회전하는 큐

덱을 활용하여 큐를 회전시키는 문제

<특이사항>

* 왼쪽에서 찾는게 더 적은 횟수를 가진다.
* 왼쪽으로 pop 할 때와 오른쪽으로 pop 할 때 카운트를 더하는 순서가 다르다.

{% highlight python %}
import sys
from collections import deque
input = sys.stdin.readline

N, M = map(int, input().split())
number_q = deque(range(1,N+1))
pick_q = deque(list(map(int, input().split())))

result = 0
pop_cnt = 0
idx = 0
while pick_q:
    pick = pick_q.popleft()
    # 찾는 번호 idx 찾기
    for i in range(len(number_q)):
        if number_q[i] == pick:
            idx = i
    # 연산
    find_flag = False
    if len(number_q)//2 >= idx:
        # 왼쪽으로 이동
        while find_flag==False:
            num = number_q.popleft()
            if num == pick:
                break
            number_q.append(num)
            num = number_q
            result += 1
    else:
        # 오른쪽으로 이동
        while find_flag==False:
            result += 1
            num = number_q.pop()
            if num == pick:
                break
            number_q.appendleft(num)
            num = number_q
print(result)
{% endhighlight %}

## AC

덱을 활용하여 시간복잡도를 향상시키는 문제

<주의사항>

* 에러 처리
  - 갯수 n이 실제 입력값과 다를 수 있다.
  - 범위로 조건 분기하지 말고 error 변수를 선헌해서 조건 분기를 하자

{% highlight python %}
import sys
from collections import deque
input = sys.stdin.readline

T = int(input())
for _ in range(T):
    commend = input().rstrip("\n")
    n = int(input())
    q = deque(input().rstrip("\n")[1:-1].split(","))
    
    error = 0
    flag = True
    if n != len(q):
        q = []
    for cmd in commend:
        if cmd == "R":
            if flag == True:      flag = False
            else:                 flag = True
        else:
            if len(q) < 1:
                error = 1
                break
            else:
                if flag == True:   q.popleft()
                else:             q.pop()
    if error == 1:
        print("error")
    else:
        if flag == True:
            print("[" + ",".join(q) + "]")
        else:
            q.reverse()
            print("[" + ",".join(q) + "]")
{% endhighlight %}