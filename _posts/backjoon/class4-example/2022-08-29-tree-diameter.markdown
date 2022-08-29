---
layout: posts
title:  "solved.ac: CLASS 4, 트리의 지름"
date:   2022-08-29 04:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - solved.ac
  - class 4
---

# 트리의 지름

트리의 지름이란, 트리에서 임의의 두 점 사이의 거리 중 가장 긴 것을 말한다. 트리의 지름을 구하는 프로그램을 작성하시오.

트리의 정점의 개수 V가 주어지고 (2 ≤ V ≤ 100,000)둘째 줄부터 V개의 줄에 걸쳐 간선의 정보가 다음과 7같이 주어진다.

-> DFS, BFS

문제 포인트

* BFS를 이용하여 부모노드의 거리를 자식노드에 더함, 노드가 끝날 때까지 반복
* 정점이 될 수 있는 종단 노드들을 이용한 트리 지름 중 가장 긴 것을 출력
* graph 참조를 어떻게 할 것인가?
  * copy.deepcopy()함수를 이용하지 않으면 사용자 지정 함수 내에서 사용한 graph 변수가 call by reference로 참조 됨 -> 시간초과
  * distance와 관련된 변수 추가

## 첫번째시도

deep copy 때문에 시간초과가 걸리는 것으로 보인다.

{% highlight python %}
import sys
import copy
from collections import deque
sys.setrecursionlimit(10**6)
input = sys.stdin.readline

V = int(input())

# graph 생성 및 종단 정점 저장
endpoint = []
graph = [[] for _ in range(V+1)]
for _ in range(V):
    lists = list(map(int,input().split()))
    for i in range(1,len(lists)-1,2):
        graph[lists[0]].append([lists[i],lists[i+1]])
    if len(graph[lists[0]]) == 1:
        endpoint.append(lists[0])

for g in graph:
    g.sort()

# distance를 bfs를 하면서 누적, 최댓값 출력
def bfs(graph,start):
    m_graph = copy.deepcopy(graph)
    check = [False]*(V+1)
    check[start] = True
    q = deque([(start,0)])
    diameter = 0
    while q:
        v,dist = q.popleft()
        for node in m_graph[v]:
            if check[node[0]] == False:
                check[node[0]] = True
                node[1] += dist
                if node[1] >= diameter:
                    diameter = node[1]
                q.extend([(node[0],node[1])])
    return diameter

M = 0
for e in endpoint:
    diameter = bfs(graph,e)
    if diameter > M:
        M = diameter

print(M)
{% endhighlight %}

## 두번재시도

다익스트라 알고리즘 내부 distance 연산 부분을 참고하여 변수를 따로 설정해서 구현했다.
여전히 시간 초과가 발생한다.
단방향 노드를 입력하는 부분의 수정이 필요할 것 같다.

{% highlight python %}
import sys
import heapq
input = sys.stdin.readline

V = int(input())

# graph 생성 및 종단 정점 저장
endpoint = set()
graph = [[] for _ in range(V+1)]
for _ in range(V):
    lists = list(map(int,input().split()))
    for i in range(1,len(lists)-1,2):
        graph[lists[0]].append((lists[i],lists[i+1]))
    if len(graph[lists[0]]) == 1:
        endpoint.add(lists[0])

for g in graph:
    g.sort()

# distance를 bfs를 하면서 누적, 최댓값 출력
def bfs(graph,start):
    check = [False]*(V+1)
    check[start] = True
    # result: [node_num, distance], 가장 거리가 먼 노드의 번호와 거리
    result = [0,[0]*(V+1)]
    result[1][start] = 0
    q = []
    heapq.heappush(q, (start,0))
    while q:
        v, dist = heapq.heappop(q)
        for node in graph[v]:
            if check[node[0]] == False:
                check[node[0]] = True
                cost = dist + node[1]
                if cost >= result[1][node[0]]:
                    result[0] = node[0]
                    result[1][node[0]] = cost
                heapq.heappush(q, (node[0], cost))
    return result[0], max(result[1])

# 단방향 노드 중 최댓값 출력
M = 0
while endpoint:
    e = list(endpoint)[0]
    max_endpoint, distance = bfs(graph,e)
    endpoint.remove(e)
    endpoint.discard(max_endpoint)
    if distance > M:    M = distance

print(M)
{% endhighlight %}