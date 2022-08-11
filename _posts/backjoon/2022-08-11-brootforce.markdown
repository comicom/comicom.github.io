---
layout: posts
title:  "Broot Force"
date:   2022-08-11 12:10:28 +0900
categories: Backjoon
tags:
  - python
  - brootforce
---

# Introduction

**무차별 대입 공격**

## product
{% highlight python %}
from itertools import product
list = product(A, repeeat=B)
{% endhighlight %}

A는 조합을 만들 내용 입력, B는 자릿수 입력
* 여러 리스트들의 조합을 만들기 위해 사용
* 문자열을 입력할 경우, 문자열 원소 하나하나를 인식하여 조합의 재료로 사용

### 데카르트곱
{% highlight python %}
from itertools import product

iterator1 = [1, 2, 3]
iterator2 = ['A', 'B', 'C']

print(list(product(iterator1, iterator2)))

>>> [(1, 'A'), (1, 'B'), (1, 'C'), (2, 'A'), (2, 'B'), (2, 'C'), (3, 'A'), (3, 'B'), (3, 'C')]

print([(i,j) for i in iterator1 for j in iterator2])

>>> [(1, 'A'), (1, 'B'), (1, 'C'), (2, 'A'), (2, 'B'), (2, 'C'), (3, 'A'), (3, 'B'), (3, 'C')]
{% endhighlight %}

### 중복 순열(순서O, 중복O)
{% highlight python %}
from itertools import product

iterator = ['A','B','C','D','E']

print(list(product(iterator, repeat = 1)))

>>> [('A',), ('B',), ('C',), ('D',), ('E',)]

print(list(product(iterator, repeat = 2)))

>>> [('A', 'A'), ('A', 'B'), ('A', 'C'), ('A', 'D'), ('A', 'E'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('B', 'D'), ('B', 'E'), ('C', 'A'), ('C', 'B'), ('C', 'C'), ('C', 'D'), ('C', 'E'), ('D', 'A'), ('D', 'B'), ('D', 'C'), ('D', 'D'), ('D', 'E'), ('E', 'A'), ('E', 'B'), ('E', 'C'), ('E', 'D'), ('E', 'E')]
{% endhighlight %}

## permutations (순서O, 중복X) - 순열
{% highlight python %}
from itertools import permutations

iterator = ['A','B','C']

print(list(permutations(iterator)))

>>> [('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]

print(list(permutations(iterator, 2)))

>>> [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
{% endhighlight %}

## combinations (순서X, 중복X) - 조합
{% highlight python %}
from itertools import combinations

iterator = ['A','B','C']

print(list(combinations(iterator, len(iterator))))

>>> [('A', 'B', 'C')]

print(list(combinations(iterator, 2)))

>>> [('A', 'B'), ('A', 'C'), ('B', 'C')]
{% endhighlight %}


{% highlight python %}
import time
from itertools import product

password = "world1"
number = "0123456789"
lowercase = "abcdefghijklmnopqrstuvwxyz"
uppercase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
symbol = "!@#$%^&*()_+-=`~"
possibility = lowercase + number
attempt = product(possibility, repeat=len(password))
start = time.time()

def run():
    for i in attempt:
        if "".join(i) == password:
            print("비밀번호 : " + str("".join(i)))
            print("소요시간 : " + str(time.time() - start))

run()
{% endhighlight %}

# Example
https://www.acmicpc.net/step/22

## 블랙잭
{% highlight python %}
from itertools import combinations

N, M = map(int, input().split(' '))
cards = list(map(int, input().split(' ')))

output = 0

for card in combinations(cards, 3):
    val = card[0]+card[1]+card[2]
    if M >= val and output < val:
        output = val

print(output)
{% endhighlight %}

## 분배합
{% highlight python %}
num = int(input())

output = 0
for n in range(num):
    sum = 0
    for i in str(n):
        sum += int(i)
    if n+sum == num:
        output=n
        break

print(output)
{% endhighlight %}

## 덩치
{% highlight python %}
N = int(input())
people = []
for i in range(N):
    people.append(list(map(int,input().split(' '))))

output = []
for p in people:
    k=1
    for other in people:
        if p[0]<other[0] and p[1]<other[1]:
            k+=1
    output.append(k)

result = ''
for i in output:
    result = result + str(i) + ' '

print(result[:-1])
{% endhighlight %}

## 체스판 다시 칠하기
{% highlight python %}

{% endhighlight %}

## 영화감독 숌
{% highlight python %}

{% endhighlight %}