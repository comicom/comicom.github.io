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

### N과 M 1

https://www.acmicpc.net/problem/15649

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열

#### python itertools, premutation (순서O, 중복X) = 순열

{% highlight python %}
iterator = ['A','B','C']

print(list(permutations(iterator)))

>>> [('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]

print(list(permutations(iterator, 2)))

>>> [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
{% endhighlight %}

#### 해답

{% highlight python %}
import sys
from itertools import permutations
input = sys.stdin.readline

N, M = map(int,input().split())

output = sorted(list(permutations(range(1,N+1),M)))
for out in output:
    string = ''
    for o in out:
        string = string + str(o) + ' '
    print(string[:-1])
{% endhighlight %}

### N과 M 2

https://www.acmicpc.net/problem/15650

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

* 1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열
* 고른 수열은 오름차순이어야 한다.

#### python itertools, combinations (순서X, 중복X) = 조합

{% highlight python %}
iterator = ['A','B','C']

print(list(permutations(iterator)))

>>> [('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]

print(list(permutations(iterator, 2)))

>>> [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
{% endhighlight %}

#### 해답

{% highlight python %}
import sys
from itertools import combinations
input = sys.stdin.readline

N, M = map(int,input().split())

output = sorted(list(combinations(range(1,N+1),M)))
for out in output:
    string = ''
    for o in out:
        string = string + str(o) + ' '
    print(string[:-1])
{% endhighlight %}

### N과 M 3

https://www.acmicpc.net/problem/15650

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

* 1부터 N까지 자연수 중에서 M개를 고른 수열
* 같은 수를 여러 번 골라도 된다.

#### python itertools, product (순서O, 중복O)

{% highlight python %}
from itertools import product

iterator = ['A','B','C','D','E']

print(list(product(iterator, repeat = 1)))

>>> [('A',), ('B',), ('C',), ('D',), ('E',)]

print(list(product(iterator, repeat = 2)))

>>> [('A', 'A'), ('A', 'B'), ('A', 'C'), ('A', 'D'), ('A', 'E'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('B', 'D'), ('B', 'E'), ('C', 'A'), ('C', 'B'), ('C', 'C'), ('C', 'D'), ('C', 'E'), ('D', 'A'), ('D', 'B'), ('D', 'C'), ('D', 'D'), ('D', 'E'), ('E', 'A'), ('E', 'B'), ('E', 'C'), ('E', 'D'), ('E', 'E')]
{% endhighlight %}

#### 해답

{% highlight python %}
import sys
from itertools import product
input = sys.stdin.readline

N, M = map(int,input().split())

output = sorted(list(product(range(1,N+1),repeat=M)))
for out in output:
    string = ''
    for o in out:
        string = string + str(o) + ' '
    print(string[:-1])
{% endhighlight %}

### N과 M 4

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

* 1부터 N까지 자연수 중에서 M개를 고른 수열
* 같은 수를 여러 번 골라도 된다.
* 고른 수열은 비내림차순이어야 한다.
    * 길이가 K인 수열 A가 A1 ≤ A2 ≤ ... ≤ AK-1 ≤ AK를 만족하면, 비내림차순이라고 한다.

#### 첫번째시도

메모리초과

product 함수를 쓰지 말고 직접 구현해야 할 것 같다.

{% highlight python %}
import sys
from itertools import product
input = sys.stdin.readline

N, M = map(int,input().split())

output = set(product(range(1,N+1),repeat=M))
result = []
for out in output:
    flag = True
    pre_o = out[0]
    for o in out:
        if pre_o > o:
            flag = False
            break
        pre_o = o
    if flag == True:
        result.append(out)

result.sort()
for res in result:
    string = ''
    for r in res:
        string = string + str(r) + ' '
    print(string[:-1])
{% endhighlight %}

### N과 M 5

{% highlight python %}
import sys
from itertools import permutations 
input = sys.stdin.readline

N, M = map(int,input().split())
numbers = map(int,input().split())

output = sorted(list(permutations(numbers,M)))

for out in output:
    string = ''
    for o in out:
        string = string + str(o) +' '
    print(string[:-1])
{% endhighlight %}

### N과 M 6

{% highlight python %}
import sys
from itertools import combinations 
input = sys.stdin.readline

N, M = map(int,input().split())
numbers = list(map(int,input().split()))

numbers.sort()
output = list(combinations(numbers,M))

for out in output:
    string = ''
    for o in out:
        string = string + str(o) +' '
    print(string[:-1])
{% endhighlight %}

### N과 M 7

{% highlight python %}
import sys
from itertools import product 
input = sys.stdin.readline

N, M = map(int,input().split())
numbers = list(map(int,input().split()))

numbers.sort()
output = list(product(numbers,repeat=M))

for out in output:
    string = ''
    for o in out:
        string = string + str(o) +' '
    print(string[:-1])
{% endhighlight %}

### N과 M 8

N과 M 4 문제와 비슷함

### N과 M 9
### N과 M 10
### N과 M 11
### N과 M 12

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