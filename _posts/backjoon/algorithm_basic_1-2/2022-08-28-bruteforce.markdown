---
layout: posts
title:  "Backjoon Algorithm 1-2: Brute Force"
date:   2022-08-28 12:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - brute force
---

# Introduction

시간초과를 생각하지 말고 일단 구현하자.

## Basic

### 일곱 난쟁이

https://www.acmicpc.net/problem/2309

{% highlight python %}
import sys
input = sys.stdin.readline

lists = []
for _ in range(9):
    lists.append(int(input()))

over = sum(lists) - 100
lists.sort()

findFlag = False
for i in range(len(lists)-1,-1,-1):
    for j in range(0,len(lists),1):
        if lists[i]+lists[j] > over:
            break
        if lists[i]+lists[j] == over:
            if i > j:
              lists.pop(i)
              lists.pop(j)
            else:
              lists.pop(j)
              lists.pop(j)
            findFlag = True
            break
    if findFlag == True:
        break

for l in lists:
    print(l)
{% endhighlight %}

### 사탕 게임

https://www.acmicpc.net/problem/3085

{% highlight python %}
import sys
input = sys.stdin.readline

# 값 초기화
N = int(input())

candy = [['']*N for _ in range(N)]

for i in range(N):
    candy_string = input().rstrip("\n")
    for c in range(len(candy_string)):
      candy[i][c] = candy_string[c]

# 구현
{% endhighlight %}

## N과 M

## 순열

## 재귀

## 비트마스크

### 집합

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


* 풀이

주의) sys.stdin.readline을 쓰지 않으면 시간초과가 된다.

{% highlight python %}
import sys
input = sys.stdin.readline

# 값 초기화
N = int(input())

S = set()
cmd = []
for _ in range(N):
    cmd = input().split()
    if cmd[0] == "add":
        if int(cmd[1]) not in S:    S.add(int(cmd[1]))
    if cmd[0] == "remove":
        if int(cmd[1]) in S:        S.remove(int(cmd[1]))
    if cmd[0] == "check":
        if int(cmd[1]) in S:
            print(1)
        else:
            print(0)
    if cmd[0] == "toggle":
        if int(cmd[1]) in S:        S.remove(int(cmd[1]))
        elif int(cmd[1]) not in S:  S.add(int(cmd[1]))
    if cmd[0] == "all":
        S = set([1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20])
    if cmd[0] == "empty":
        S = set()
{% endhighlight %}