---
layout: post
title: 병합정렬(Merge Sort)
categories: [Programming]
tags: [Programming, Algorithm]
fullview: false
comments: true
published: true
use_math: false
---

여러 개의 정렬된 자료의 집합을 결합하여 한 개의 정렬된 집합으로 만드는 방법이다. 병합 정렬은 전체 원소들에 대해서 수행하지 않고 부분집합으로 분할 하고 각 부분집합에 대해서 정렬 작업을 완성한 후에 정렬된 부분집합들을 다시 결합하는 분할 정복 기법을 사용한다.

2개의 정렬된 자료의 집합을 결합하여 하나의 집합으로 만드는 병합 방법을 2-way 병합이라 하고, n개의 정렬된 자료의 집합을 결합하여 하나의 집합으로 만드는 병합 방법을 n-way 병합이라고 한다. 2-way 병합 정렬은 다음과 같은 작업을 반복 수행하면서 완성한다.

 ```python
def mergeSort(alist):
  print("Splitting ", alist)
  if len(alist)&gt;1:
    mid = len(alist)//2
    lefthalf = alist[:mid]
    righthalf = alist[mid:]

    mergeSort(lefthalf)
    mergeSort(righthalf)

    i = 0
    j = 0
    k = 0

    while i &lt; len(lefthalf) and j &lt; len(righthalf):
      if lefthalf[i]  &lt; righthalf[j]:
        alist[k] = lefthalf[i]
        i = i + 1
      else:
        alist[k] = righthalf[j]
        j = j + 1
      k = k + 1

    while i &lt; len(lefthalf):
      alist[k] = lefthalf[i]
      i = i + 1
      k = k + 1
  print("Merging ", alist)

alist = [6, 2, 4, 1, 3, 7, 5, 8]
mergeSort(alist)
print(alist)
```
