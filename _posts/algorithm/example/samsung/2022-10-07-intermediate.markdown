---
layout: posts
title:  "Programming - Advanced"
date:   2022-10-07 07:10:28 +0900
categories: SWExpert
tags:
  - python
  - algorithm
  - sw expert academy
---

# Introduction

https://swexpertacademy.com/main/learn/course/subjectList.do?courseId=AVuPDYSqAAbw5UW6

## 구현 6, 그래프의 기본과 탐색

### 그래프

* 객체(사물 또는 추상적 개념)들과 객체들 사이의 연결 관계 표현
* 정점들의 집합과 정점을 연겨하는 간선들의 집합으로 구성된 자료 구조
* 선형 자료구조나 트리 자료구조로 표현하기 어려운 N:N 관계를 가지는 원소들을 표현하기에 용이

* 무향 그래프: 서로 대칭적인 관계를 연결해서 나타낸 그래프
* 유향 그래프: 서로 대칭적이지 않은 관계 표현
    * 기업 간의 공급 관계, 작업의 선후 관계 등 표현
    * 가중치 그래프: 이동하는데 드는 비용을 가중치로 표현한 그래프

* 경로: 간선들을 순서대로 나열한것
* 단순경로: 경로 중 한 정점을 최대한 한 번만 지나는 경로
* 사이클: 시작한 정점에서 끝나는 경로
* 사이클 없는 유향 그래프(DAG)

* 인접행렬
* 인접리스트

### 그래프 탐색

* 깊이우선탐색(DFS)
    * visited를 이용하여 재방문 여부 판단
    * 재귀
    * 반복: stack 사용
* 너비우선탐색(BFS)
    * 반복: queue, heap

### 상호배타 집합들

* 서로 중복 포함된 원소가 없는 집합들로 **교집합이 없음**
* 집합에 속한 하나의 특정 원소를 통해 각 집합들을 구분
* 상호배타 집합을 표현하는 방법
    * 연결 리스트
    * 트리

* make-set(x): 원소 x만으로 구성된 집합을 생성하는 연산
* find-set(x): 임의의 원소 x가 속한 집합을 알아내기 위해 사용하며, 집합의 대표자를 알기 위한 연산
* union(x,y): x 원소가 속한 집합과 y 원소가 속한 집합을 하나의 집합으로 합치는 연산

연산 효율 높히기

* Rank를 이용한 Union
* Path compression

* 그래프의 연결성을 확인할 때 사용
* 크루스칼 알고리즘에 사용
* 각 집합에 속한 원소의 수 관리할 때 사용
    * 가장 큰 집합 추적하기
    * 집합의 노드 개수가 몇 개 이상이 되는 시점 찾기

## 구현 7, 그래프의 최소 비용 문제

### 최소 신장 트리

* 간선들의 가중치 합이 최소가 되는 트리를 찾는 문제
    * 프림: 선택한 정점들과 인접하는 정점들 중 최소 비용의 간선이 존재하는 정점 선택
    * 크루스칼: 최소 가중치 간선을 하나씩 선택해서 최소 신장트리를 찾는 알고리즘
        * 최초, 모든 간선을 가중치에 따라 오름차순 정렬
        * 가중치가 가장 낮은 간선부터 선택하면서 트리 증가 (사이클이 존재하면 다음으로 가중치가 낮은 간선 선택)
        * N-1개의 간선이 선택될 때 까지 두 번째 과정을 반복

{% highlight python %}
# 프림 알고리즘
def MST_PRIM(G,s):
    key = [INF]*N
    pi = [None]*N
    visited = [False]*N
    key[s] = 0

    for _ in range(N):
        minIndex = -1
        min = INF
        for i in range(N):
        if not visited[i] and and key[i] < min:
            min = key[i]
            minIndex = i
        visited[minIndex] = True
        for v, val in G[minIndex]:
            if not visited[v] and val < key[v]:
                key[v] = val
                pi[v] = minIndex

# 크루스칼 알고리즘
def MST_KRUSKAL(G):
    mst = []
    for i in range9N):
        make_set(i)
    G.sort(key = lambda t: t[2])
    mst_cost=0

    while len(mst) < N-1:
        u,v,val = G.pop(0)
        if find_set(u) != find_set(v):
            union(u,v)
            mst_append((u,v))
            mst_cost += val
{% endhighlight %}
* 시작 정점 목표 정점까지 가는 간선의 가중치 합이 최소가 되는 경로를 찾는 문제

### 최단 경로

간선의 가중치가 있는 유향 그래프에서 두 정점 사이의 경로들 중 간선의 가중치의 합이 최소인 경로

* 출발점에서 다른 모든 정점들에 이르는 최단 경로를 구하는 문제
    * 다익스트라, 음의 가중치 허용하지 않음
    * 벨만포드, 음의 가중치 허용 + 가중치 합이 음인 사이클 허용 X
* 모든 쌍 최단 경로 문제
    * 플로이드 워셜

{% highlight python %}
# 다익스트라 알고리즘
def Dijkstra(G,R):
    D = [INF]*N
    P = [None]*N
    visited = [False]*N
    D[r] = 0

    for _ in range(N):
        minIndex = -1
        min = INF
        for i in range(N):
            if not visited[i] and D[i] < min:
                min = D[i]
                minIndex = i
        visited[minIndex] = True
        for v, val in G[minIndex]:
            if not visited[v] and D[minIndex] + val < D[v]:
                D[v] = D[minIndex] + val
                P[v] = minIndex

# 크루스칼 알고리즘
def MST_KRUSKAL(G):
    mst = []
    for i in range9N):
        make_set(i)
    G.sort(key = lambda t: t[2])
    mst_cost=0

    while len(mst) < N-1:
        u,v,val = G.pop(0)
        if find_set(u) != find_set(v):
            union(u,v)
            mst_append((u,v))
            mst_cost += val
{% endhighlight %}

## String


