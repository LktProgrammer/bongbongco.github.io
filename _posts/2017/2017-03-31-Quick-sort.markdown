---
layout: post
title: 퀵 정렬(Quick Sort)
categories: [Programming]
tags: [Programming, Algorithm]
fullview: false
comments: true
published: true
use_math: false
---

정렬할 전체 원소에 대해서 정렬을 수행하지 않는다. 먼저 기준값을 중심으로 전체 원소들을 왼쪽 부분집합과 오른쪽 부분집합으로 분할한다. 왼쪽 부분집합에는 기준값보다 작은 원소들을 이동시키고, 오른쪽 부분집합에는 기준값보다 큰 원소들을 이동시킨다. 이때 사용하는 기준값을 피봇이라고 하는데, 일반적으로 전체 원소 중에서 가운데에 위치한 원소를 피봇으로 선택한다.

퀵 정렬은 다음의 두 가지 기본 작업을 반복 수행하여 완성한다.

(1) 분할 : 정렬할 자료들을 기준값을 중심으로 2개의 부분집합으로 분할한다.
(2) 정복 : 부분집합의 원소들 중에서 기준값보다 작은 원소들은 왼쪽 부분집합으로, 기준값보다 큰 원소들은 오른쪽 부분집합으로 정렬한다. 부분집합의 크기가 1 이하로 충분히 작지 않으면 순환 호출을 이용하여 다시 분할한다.

 
```python
import unittest

def quick_sort(list, start, end):
  if start &lt; end:
    pivot = partition(list, start, end)
    quick_sort(list, start, pivot-1)
    quick_sort(list, pivot+1, end)
  return list

def partition(list, start, end):
  pivot = end
  wall = start
  left = start

  while left &lt; pivot:
    if list[left] &lt; list[pivot]:
      list[wall], list[left] = list[left], list[wall]
      wall = wall + 1
    left = left + 1

  list[wall], list[pivot] = list[pivot], list[wall]
  pivot = wall
  return pivot

class unit_test(unittest.TestCase):
  def test(self):
    list = [8, 13, 2, 6, 1, 4]
    self.assertEqual([1, 2, 4, 6, 8, 13], quick_sort(list, 0, len(list)-1))
``` 
