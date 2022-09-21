---
layout: posts
title:  "Stack"
date:   2022-09-04 12:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - stack
---

# Introduction

재귀함수를 다뤄 봅시다.

# Example

https://www.acmicpc.net/step/19

## 재귀함수가 뭔가요?

재귀함수를 배우면서 재귀함수를 배우는 문제

{% highlight python %}
import sys
input = sys.stdin.readline

N = int(input())

def recursion(cnt,n):
    print("____"*cnt+'"재귀함수가 뭔가요?"')
    if cnt == n:
        print("____"*cnt+'"재귀함수는 자기 자신을 호출하는 함수라네"')
    else:
        print("____"*cnt+'"잘 들어보게. 옛날옛날 한 산 꼭대기에 이세상 모든 지식을 통달한 선인이 있었어.')
        print("____"*cnt+'마을 사람들은 모두 그 선인에게 수많은 질문을 했고, 모두 지혜롭게 대답해 주었지.')
        print("____"*cnt+'그의 답은 대부분 옳았다고 하네. 그런데 어느 날, 그 선인에게 한 선비가 찾아와서 물었어."')
        recursion(cnt+1,n)
    print("____"*cnt+"라고 답변하였지.")

print("어느 한 컴퓨터공학과 학생이 유명한 교수님을 찾아가 물었다.")
recursion(0,N)
{% endhighlight %}

## 재귀의 귀재

{% highlight python %}
import sys
input = sys.stdin.readline

cnt = 0
def recursion(s, l, r):
    global cnt
    cnt += 1
    if l >= r:          return 1
    elif s[l] != s[r]:  return 0
    else:               return recursion(s, l+1, r-1)

def isPalindrome(s):
    return recursion(s,0,len(s)-1)

T = int(input())
for _ in range(T):
    string = input().rstrip("\n")
    cnt = 0
    print(isPalindrome(string),cnt)
{% endhighlight %}

## 병합정렬

{% highlight python %}
{% endhighlight %}

## 별 찍기 - 10

재귀적인 패턴을 재귀함수로 찍는 문제

{% highlight python %}
## star(3)  3x3
## star(9)  9x9
# star(3), star(3), star(3)
# star(3),    X   , star(3)
# star(3), star(3), star(3)
## star(27)  27x27
# star(9), star(9), star(9)
# star(9),    X   , star(9)
# star(9), star(9), star(9)
{% endhighlight %}

## 하노이탑 이동 순서

재귀적인 패턴을 찾아서 재귀함수로 찍는 문제