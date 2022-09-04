---
layout: posts
title:  "Binary Search"
date:   2022-08-11 12:10:28 +0900
categories: Backjoon
tags:
  - python
  - algorithm
  - binary search
---

# Introduction

* 탐색 리스트가 정렬이 되어 있지 않다면 정렬
* left, right, mid를 잡아줌 (리스트 첫 번째는 left, 마지막은 right, 중간값은 mid)
* mid 값과 찾고자 하는 값 비교
    * mid값이 더 크면 right 값을 mid-1, mid 값이 더 작으면 left 값을 mid+1로 세팅
* left > right가 될 때 까지 반복

{% highlight python %}
def binary_search(arr, value):
    first, last = 0, len(arr)

    while first <= last:
        mid = (first + last) // 2
        if arr[mid] == value:
            return mid
        if arr[mid] > value:
            last = mid - 1
        else:
            first = mid + 1

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
result_index = binary_search(arr, 6)
print(result_index, arr[result_index])
{% endhighlight %}