---
layout: posts
title:  "정수론과 조합론"
date:   2022-08-29 07:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - number theory
  - combinatorism
---

# Introduction

정수론과 조합론을 배워 봅시다.

# Example

https://www.acmicpc.net/step/18

## 배수와 약수

{% highlight python %}
import sys
input = sys.stdin.readline

a, b = map(int,input().split())
while a!=0 and b!=0:
    if a < b and b%a == 0:
        print("factor")
    elif a > b and a%b == 0:
        print("multiple")
    else:
        print("neither")
    a, b = map(int,input().split())
{% endhighlight %}

## 약수

입력된 값을 정렬하고 첫 값과 끝 값을 곱해주면 된다.

{% highlight python %}
import sys
input = sys.stdin.readline

N = int(input())
numbers = list(map(int,input().split()))
numbers.sort()
print(numbers[0]*numbers[-1])
{% endhighlight %}

## 최소공배수

GDB 공식 사용해서 문제 해결

최소공약수: 2개의 자연수 a, b(a>b)에 대해서 a를 b로 나눈 나머지가 r일 때, a와 b의 최대공약수는 b와 r의 최대공약수와 같다.

최대공배수: 각 수를 곱한 값에 최소공약수를 나눈 값


{% highlight python %}
import sys
input = sys.stdin.readline

def gdb(big,small):
    r = big%small
    while r!=0:
      big = small
      small = r
      r = big%small
    return small

T = int(input())
for _ in range(T):
    A, B = map(int,input().split())
    if A>B:
        print(int(A*B/gdb(A,B)))
    else:
        print(int(A*B/gdb(B,A)))
{% endhighlight %}

## 검문

### 첫번째시도

공식이 떠오르지 않아서 일단 구현했다.

시간초과

{% highlight python %}
import sys
input = sys.stdin.readline

N = int(input())

numbers = []
for _ in range(N):
    numbers.append(int(input()))
numbers.sort()

output = []
for i in range(1,numbers[-1]+1):
    flag = True
    val = numbers[0]%i
    for n in numbers:
        if n%i != val:
            flag = False
            break
    if flag == True:
        output.append(i)

result = ''
for o in output[1:]:
    result = result + str(o) + ' '
print(result[:-1])
{% endhighlight %}

## 링

## 이항 계수1

이항계수: 조합론에서 등장하는 개념으로, 주어진 크기 집합에서 원하는 개수만큼 순서없이 뽑는 조합의 가지수

* 이항계수는 nCr이다
* nCr = n!/k!(n-k)!

python >= 3.8
{% highlight python %}
import math
print(math.comb(10,5))
{% endhighlight %}

기타
{% highlight python %}
from math import factorial as fact
print(fack(n)//(fack(k)*fack(n-k)))
{% endhighlight %}

문제

{% highlight python %}
import sys
from math import factorial as fact
input = sys.stdin.readline

N, K = map(int,input().split())

result = fact(N)//(fact(K)*fact(N-K))
print(result)
{% endhighlight %}

## 이항 계수2

## 다리 놓기

## 패션왕 신해빈

## 조합 0의 개수

시간초과

{% highlight python %}
import sys
from math import factorial as fact
input = sys.stdin.readline

n, m = map(int,input().split())

result = str(fact(n)//(fact(m)*fact(n-m)))

cnt = 0
for i in range(len(result)-1,-1,-1):
    if result[i] == '0':
        cnt += 1
    else:
        break
print(cnt)
{% endhighlight %}