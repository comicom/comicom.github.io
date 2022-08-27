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

## Basic
### 스택
https://www.acmicpc.net/problem/10828

stack은 LIFO(Last Input First Out)구조이다.
따라서 pop 할 때 append 된 항목이 출력되어야 한다. 

{% highlight python %}
import sys
input = sys.stdin.readline
N = int(input())

stack = []
commend = []
for _ in range(N):
    commend = list(input().split())
    if commend[0]=="push":
        stack.append(int(commend[1]))
    if commend[0]=="pop":
        if len(stack) == 0:
            print(-1)
        else:
            print(stack.pop())
    if commend[0]=="size":
        print(len(stack))
    if commend[0]=="empty":
        if len(stack) == 0:
            print(1)
        else:
            print(0)
    if commend[0]=="top":
        if len(stack) == 0:
            print(-1)
        else:
            print(stack[-1])
{% endhighlight %}

note.

위 문제는 파이썬에서 기본적으로 제공되는 linked list 자료구조로 구현한 것이다.
stack module은 따로 있다. [!ref](https://runestone.academy/runestone/books/published/pythonds/BasicDS/ImplementingaStackinPython.html)
{% highlight python %}
from pythons.basic.stack import Stack
s = Stack

s. push(1)
s. push(2)
s. push(3)
print(s.items) # [1,2,3]
print(s.peek()) # 3
print(s.size()) # 3
print(s.pop()) # 3 -> [1,2]
print(s.size()) # 2
print(s.isEmppty()) # False
{% endhighlight %}

### 단어 뒤집기

https://www.acmicpc.net/problem/9093

{% highlight python %}
import sys
input = sys.stdin.readline
N = int(input())

result = ''
for _ in range(N):
  string = input().split()
  for s in string:
    for c in range(len(s)-1,-1,-1):
      result += s[c]
    result += " "
  print(result)
  result = ''
{% endhighlight %}

### 괄호

https://www.acmicpc.net/problem/9012

### 스택 수열

https://www.acmicpc.net/problem/1874

{% highlight python %}
import sys
input = sys.stdin.readline

n = int(input())

arr = []
for _ in range(n):
    num = int(input())
    arr.append(num)

# push를 진행할 때는 반드시 1, 2, 3, ... 순서대로 진행해야 한다.
# * 1, 4 이런식으로 진행 X

cnt = 1
arr_dummy = []
arr_test = []
result = []
for arr_num in arr:
    if len(arr_dummy) > 0:
        if arr_dummy[-1] == arr_num:
            arr_test.append(arr_dummy.pop())
            result.append("-")
        elif arr_dummy[-1] != arr_num:
            if arr_num not in arr_dummy and arr_num < arr_dummy[-1] or cnt > arr_num+1:
                break
            else:
                for i in range(cnt,arr_num+1):
                    arr_dummy.append(i)
                    result.append("+")
                arr_test.append(arr_dummy.pop())
                result.append("-")
                cnt = arr_num+1
    else:
        for i in range(cnt,arr_num+1):
            arr_dummy.append(i)
            result.append("+")
        arr_test.append(arr_dummy.pop())
        result.append("-")
        cnt = arr_num+1

if len(arr_test) == len(arr):
    for r in result:
        print(r)
else:
    print("NO")
{% endhighlight %}

### 에디터

### 큐

stack은 FIFO(Firts Input First Out)구조이다.
따라서 pop 할 때 첫 번째 인덱스에 있는 값이 출력되어야 한다.

{% highlight python %}
import sys
input = sys.stdin.readline

N = int(input())

lists = []
for _ in range(N):
    cmd = input().split()
    if cmd[0] == "push":
        lists.append(int(cmd[1]))
    if cmd[0] == "pop":
        if len(lists)>0:
            print(lists.pop(0))
        else:
            print(-1)
    if cmd[0] == "size":
        print(len(lists))
    if cmd[0] == "empty":
        if len(lists)==0:
            print(1)
        else:
            print(0)
    if cmd[0] == "front":
        if len(lists)>0:
            print(lists[0])
        else:
            print(-1)
    if cmd[0] == "back":
        if len(lists)>0:
            print(lists[-1])
        else:
            print(-1)
{% endhighlight %}

note.

위 문제는 파이썬에서 기본적으로 제공되는 linked list 자료구조로 구현한 것이다.
queue module은 따로 있다. [!ref](https://docs.python.org/ko/3.7/library/queue.html)

### 조세퍼스 문제

### 덱

https://www.acmicpc.net/problem/10866

{% highlight python %}
from collections import deque
import sys
input = sys.stdin.readline

N = int(input())

d = deque()
for _ in range(N):
    cmd = input().split()
    if cmd[0] == "push_front":
        d.appendleft(int(cmd[1]))
    if cmd[0] == "push_back":
        d.append(int(cmd[1]))
    if cmd[0] == "pop_front":
        if len(d) > 0:
            print(d.popleft())
        else:
            print(-1)
    if cmd[0] == "pop_back":
        if len(d) > 0:
            print(d.pop())
        else:
            print(-1)
    if cmd[0] == "size":
        print(len(d))
    if cmd[0] == "empty":
        if len(d) == 0:
            print(1)
        else:
            print(0)
    if cmd[0] == "front":
        if len(d) > 0:
            print(d[0])
        else:
            print(-1)
    if cmd[0] == "back":
        if len(d) > 0:
            print(d[-1])
        else:
            print(-1)
{% endhighlight %}

## Practice

### 단어 뒤집기2

### 쇠막대기

### 오큰수

### 오등큰수

## Plus

### 후위 표기식2

### 후위 표기식

### 알파벳 개수

### 알파벳 찾기

### 문자열 분석

### 단어 길이 재기

### ROT13

### 네 수

### 접미사 배열