---
layout: posts
title:  "알고리즘 수업"
date:   2022-08-11 12:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - tree
---

# Introduction

https://www.acmicpc.net/problemset?search=%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98+%EC%88%98%EC%97%85

## 피보나치 수 1

{% highlight python %}
import sys
input = sys.stdin.readline

N = int(input())

r_cnt = 1
def recursion(n):
    global r_cnt
    if n == 1 or n == 2:
        return 1
    else:
        r_cnt += 1
        return recursion(n-1) - recursion(n-2)

def dp(n):
    d = [0]*(n+1)
    d[1] = 1
    d[2] = 1

    dp_cnt = 0
    for x in range(3,n+1):
        d[x] = d[x-1] + d[x-2]
        dp_cnt += 1
    
    return dp_cnt

recursion(N)
print(r_cnt,dp(N))
{% endhighlight %}

## 피보나치 수 2