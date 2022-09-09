---
layout: posts
title:  "Floyd-Warshall"
date:   2022-09-05 12:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - floyd-warshall
---

# Introduction

그래프에서 모든 꼭짓점 사이의 최단 경로의 거리를 구하는 알고리즘.

음수 가중치를 갖는 간선도 순환만 없다면 잘 처리된다.

시간 복잡도는 O(V^3)이다


* 최단 거리 테이블 내 특정 노드에서 자기 자신 노드로 가는 비용은 항상 0이므로 대각 행렬의 값은 모두 0으로 초기화합니다.
* 특정 노드에서 다른 모든 노드로 가는 비용(간선)에 따라 최단 거리 테이블을 갱신합니다. 노드 간에 간선으로 연결되어 있지 않은 경우에는 '무한'으로 테이블을 초기화합니다.
* 이제 1번 노드부터 차례대로 해당 노드를 중간에 거쳐서 가는 모든 노드 간의 최단 경로를 계산하고 최단 거리 테이블을 갱신합니다. 최단 거리 테이블 내 특정 노드에서 자기 자신 노드로 가는 비용은 항상 0이므로 대각 행렬의 값은 모두 0으로 초기화합니다.
* 특정 노드에서 다른 모든 노드로 가는 비용(간선)에 따라 최단 거리 테이블을 갱신합니다. 노드 간에 간선으로 연결되어 있지 않은 경우에는 '무한'으로 테이블을 초기화합니다.
* 이제 1번 노드부터 차례대로 해당 노드를 중간에 거쳐서 가는 모든 노드 간의 최단 경로를 계산하고 최단 거리 테이블을 갱신합니다. 


{% highlight python %}
import sys
input = sys.stdin.readline

n = int(input())
m = int(input())

# 인접행렬 생성
INF = (1e9)
min_dist_table = [[INF]*(n+1) for _ in range(n+1)]

for a in range(1, n+1):
    for b in range(1, n+1):
        if a == b:
            min_dist_table[a][b] =0

for _ in range(m):
    a, b, c = map(int,input().split())
    min_dist_table[a][b] = min(min_dist_table[a][b],c)

## 플로이드 워셜 알고리즘 (점화식 기반)
# 경로
for k in range(1, n+1):
    # 출발
    for a in range(1, n+1):
        # 도착
        for b in range(1, n+1):
            min_dist_table[a][b] = min(min_dist_table[a][b], min_dist_table[a][k] + min_dist_table[k][b])

# 결과 출력
for a in range(1, n + 1):
    for b in range(1, n +1):
        # 노드를 방문할 수 없는 경우, '무한' 값 출력
        if min_dist_table[a][b] == INF:
            print(0, end = ' ')
        else:
            # 노드를 방문할 수 있을 경우 최단 거리 출력
            print(min_dist_table[a][b], end = ' ')
    # 개행1
    print()
{% endhighlight %}