---
layout: posts
title:  "Divide Conquer"
date:   2022-09-04 12:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - divide conquer
---

# Introduction

재귀를 응용하는 알고리즘, 분할 정복을 익혀 봅시다.

# Example

https://www.acmicpc.net/step/20

## 색종이 만들기

쿼드트리를 만드는 문제

## 쿼드트리

쿼드트리를 문자열로 바꾸는 문제

## 종이의 개수

쿼드트리와 비슷한데 4개 대신 9개로 나누는 문제

## 곱셈

분할 정복으로 거듭제곱을 빠르게 계산하는 문제

시간 초과

{% highlight python %}import sys
sys.setrecursionlimit(10**6)
input = sys.stdin.readline

# C**1 = C
# C**2 = C*C
# C**3 = C*C*C = C**2*C
# C**4 = C*C*C*C = C**2*C**2
def Recursive_Power(num,squre):
    if squre == 1:
        return num
    if squre%2 == 0:
        result = Recursive_Power(num,squre/2)
        return result*result
    else:
        result = Recursive_Power(num,(squre-1)/2)
        return result*result*num

A, B, C = map(int,input().split())
print(Recursive_Power(A,B)%C)
{% endhighlight %}

## 이항 계수 3

분할 정복을 사용한 거듭제곱과 페르마의 소정리를 이용해 곱셈의 역원을 구하는 문제

## 행렬 곱셈

행렬의 거듭제곱을 계산하기 전에 먼저 풀어야 할 문제

## 행렬 제곱

분할 정복으로 행렬의 거듭제곱을 빠르게 계산하는 문제

## 피보나치 수 6

행렬 곱셈을 응용해 피보나치 수를 구하는 문제

## 히스토그램에서 가장 큰 직사각형

히스토그램에서 가장 큰 직사각형을 찾는 문제. (※인터넷에 널리 알려져 있는 풀이와 달리, 분할 정복 과정에서 어떠한 자료구조도 필요 없습니다.)