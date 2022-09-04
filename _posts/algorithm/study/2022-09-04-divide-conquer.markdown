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

* 동적 계획법은 분할한 문제들이 서로 영향을 미침.
* 분할 정복은 분할한 문제들이 서로 영향을 미치지 않음.

##

## 쿼드트리 문제

DFS/BFS로 탐색하고, 사각형을 구성하는 수사가 모두 같지 않다면 사각형을 네 개로 쪼개서 다시 탐색하는 과정 반복