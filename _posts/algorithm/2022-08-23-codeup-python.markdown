---
layout: posts
title:  "코드업 Python 100제"
date:   2022-08-23 12:10:28 +0900
categories: algorithm
tags:
  - python
  - algorithm
---

# Introduction

https://codeup.kr/problemsetsol.php?psid=33

## [기초-종합] 빛 섞어 색 만들기(설명)(py)

빨녹파(r, g, b) 각 빛의 가짓수가 공백을 두고 입력된다.
예를 들어, 3 3 3 은 빨녹파 빛에 대해서 각각 0~2까지 3가지 색이 있음을 의미한다.
0 <= r,g,b <= 127

만들 수 있는 rgb 색의 정보를 오름차순(계단을 올라가는 순, 12345... abcde..., 가나다라마...)으로
줄을 바꿔 모두 출력하고, 마지막에 그 개수를 출력한다.

{% highlight python %}
from itertools import product

r, g, b = map(int,input().split())

iter1 = range(r)
iter2 = range(g)
iter3 = range(b)

# 데카르트 곱연산
result = list(product(iter1,iter2,iter3))
for res in result:
  print("{0} {1} {2}".format(res[0], res[1], res[2]))
print(len(result))
{% endhighlight %}

## [기초-종합] 소리 파일 저장용량 계산하기(py)
{% highlight python %}
h, b, c, s = map(float, input().split())

mega_byte = float(h*b*c*s/8/1024/1024)

print("{0} MB".format(round(mega_byte,1)))
{% endhighlight %}

## [기초-종합] 함께 문제 푸는 날

같은 날 동시에 가입한 인원 3명이 규칙적으로 방문하는,
방문 주기가 공백을 두고 입력된다. (단, 입력값은 100이하의 자연수이다.)

3명이 다시 모두 함께 방문해 문제를 풀어보는 날(동시 가입/등업 후 며칠 후?)을 출력한다.

### 간단한 방법 (부르트포스)
{% highlight python %}
a, b, c = map(int, input().split())

d = 1
while d%a!=0 or d%b!=0 or d%c!=0 :
  d += 1
print(d)
{% endhighlight %}

### 최소공배수

## [기초-리스트] 이상한 출석 번호 부르기1(py)

{% highlight python %}
N = int(input())
number = list(map(int,input().split()))

students = [0]*23

for num in number:
    students[num-1]+=1

result = ''
for i in range(23):
  result = result + str(students[i]) + ' '
print(result[:-1])
{% endhighlight %}

## [기초-리스트] 이상한 출석 번호 부르기2(py)

{% highlight python %}
N = int(input())
number = list(map(int,input().split()))

result = ""
for i in range(len(number)-1,-1,-1):
    result = result + str(number[i]) + " "
print(result[:-1])
{% endhighlight %}

## [기초-리스트] 이상한 출석 번호 부르기3(py)

출석을 부른 번호 중에 가장 빠른 번호를 출력한다.

{% highlight python %}
N = int(input())
number = list(map(int,input().split()))

result = ""
for i in range(len(number)-1,-1,-1):
    result = result + str(number[i]) + " "
print(result[:-1])
{% endhighlight %}

## [기초-리스트] 바둑판에 흰 돌 놓기(설명)(py)

바둑판에 올려 놓을 흰 돌의 개수(n)가 첫 줄에 입력된다.
둘째 줄 부터 n+1 번째 줄까지 힌 돌을 놓을 좌표(x, y)가 n줄 입력된다.
n은 10이하의 자연수이고 x, y 좌표는 1 ~ 19 까지이며, 똑같은 좌표는 입력되지 않는다.

흰 돌이 올려진 바둑판의 상황을 출력한다.
흰 돌이 있는 위치는 1, 없는 곳은 0으로 출력한다.

{% highlight python %}
N = int(input())
go = [[0]*19 for i in range(19)]

for _ in range(N):
    y, x = map(int,input().split())
    go[x-1][y-1] = 1

result = ""
for j in range(0,19):
    for i in range(0,19):
        result = result + str(go[i][j]) + " "
    result = result[:-1] + "\n"

print(result)
{% endhighlight %}

## [기초-리스트] 바둑알 십자 뒤집기(py)

바둑알이 깔려 있는 상황이 19 * 19 크기의 정수값으로 입력된다.
십자 뒤집기 횟수(n)가 입력된다.
십자 뒤집기 좌표가 횟수(n) 만큼 입력된다. 단, n은 10이하의 자연수이다.

십자 뒤집기 결과를 출력한다.

{% highlight python %}
# go 바둑판 초기값
go = []
for _ in range(19):
  go.append(list(map(int,input().split())))

# 뒤집기 값 설정
N = int(input())
plus = []
for _ in range(N):
  iter_y, iter_x = map(int,input().split())
  plus.append((iter_x-1,iter_y-1))

# 저장된 stack이 종료될때까지 뒤집기 반복 실행
for x, y in plus:
  for i in range(0,19):
    if go[x][i]==0: go[x][i]=1
    else:           go[x][i]=0
  for i in range(0,19):
    if go[i][y]==0: go[i][y]=1
    else:           go[i][y]=0

# 결과 출력
result = ""
for j in range(0,19):
    for i in range(0,19):
        result = result + str(go[i][j]) + " "
    result = result[:-1] + "\n"

print(result)
{% endhighlight %}

## [기초-리스트] 설탕과자 뽑기(py)

첫 줄에 격자판의 세로(h), 가로(w) 가 공백을 두고 입력되고,
두 번째 줄에 놓을 수 있는 막대의 개수(n)
세 번째 줄부터 각 막대의 길이(l), 방향(d), 좌표(x, y)가 입력된다.

1 <= w, h <= 100

1 <= n <= 10

d = 0 or 1

1 <= x <= 100-h

1 <= y <= 100-w

모든 막대를 놓은 격자판의 상태를 출력한다.
막대에 의해 가려진 경우 1, 아닌 경우 0으로 출력한다.
단, 각 숫자는 공백으로 구분하여 출력한다.

{% highlight python %}
# 격자판의 세로(h), 가로(w), 막대의 개수(n), 각 막대의 길이(l),
# 막대를 놓는 방향(d:가로는 0, 세로는 1)과
# 막대를 놓는 막대의 가장 왼쪽 또는 위쪽의 위치(x, y)
w, h = map(int, input().split())
n = int(input())

# 설탕과자 설정
sugar = []
for _ in range(n):
  iter_l, iter_d, iter_y, iter_x = map(int, input().split())
  sugar.append((iter_l,iter_d,iter_x-1,iter_y-1))

board = [[0]*w for i in range(h)]

# 설탕과자 위치 입력
for l, d, x, y in sugar:
  if d == 0:
    for i in range(0,l):
      board[x+i][y] = 1
  if d == 1:
    for i in range(0,l):
      board[x][y+i] = 1

# 결과 출력
result = ""
for j in range(0,w):
    for i in range(0,h):
        result = result + str(board[i][j]) + " "
    result = result[:-1] + "\n"

print(result)
{% endhighlight %}

## [기초-리스트] 성실한 개미(py)