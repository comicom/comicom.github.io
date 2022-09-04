---
layout: posts
title:  "Binary Search"
date:   2022-09-04 12:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - binary search
---

# Introduction

https://www.acmicpc.net/step/29

## 랜선 자르기

{% highlight python %}
import sys
input = sys.stdin.readline

K, N = map(int,input().split())
lan = []
for _ in range(K):
    lan.append(int(input()))
lan.sort()

def binary_search(in_arr, answer, start, end, target):
    # 연산 부분
    # 어떤 값 x 범위 (0,max(in_arr))
    # 조건: sum([length//x for length in in_arr]) == target
    if start > end:
        return answer
    x = (start+end)//2
    # Zero Division Error 처리.
    # start와 end가 0이라는 것은 선의 길이가 1인 것과 같음
    if x == 0:
        return 1
    # 그 외
    else:
        val = sum([length//x for length in in_arr])
        if val >= target:
            answer = x
            return binary_search(in_arr, answer, x+1, end, target)
        else:
            return binary_search(in_arr, answer, start, x-1, target)

print(binary_search(lan,0,0,lan[-1],N))
{% endhighlight %}

## 나무 자르기

## 공유기 설치

## K번째 수