---
layout: post
title: 삽입정렬(Insertion Sort)
categories: [Programming]
tags: [Programming, Algorithm]
fullview: false
comments: true
published: true
use_math: false
---

정렬되어 있는 부분집합에 정렬할 새로운 원소의 위치를 찾아 삽입하는 방법이다. 삽입 정렬에서는 정렬할 자료가 두 개의 부분집합 S(Sorted)와 U(Unsorted)로 나뉘어 있다고 생각한다. 앞부분 원소부터 정렬을 수행하면서 정렬된 앞부분의 원소들은 부분집합 S가 되고 아직 정렬되지 않은 나머지 원소들은 부분집합 U가 된다. 정렬되지 않은 부분집합 U의 원소를 하나씩 꺼내서 이미 정렬되어 있는 부분집합 S의 마지막 원소부터 비교하면서 위치를 찾아 삽입하여 부분집합 S의 원소는 하나씩 늘리고 부분집합 U의 원소는 하나씩 줄인다. U의 원소를 모두 삽입하여 공집합이 되면 삽입 정렬이 완성된다.

<pre class="lang:python decode:true ">
import unittest

def insertion_sort(input):
  for idx, valueToInsert in enumerate(input):
    holePosition = idx

  while holePosition &gt; 0 and input[holePosition-1] &gt; valueToInsert:
    input[holePosition-1], input[holePosition] = input[holePosition], input[holePosition-1]
    holePosition = holePosition-1

return input

class unit_test(unittest.TestCase):
  def test(self):
    self.assertEqual(1, 2, 3, 4, 5, 6], insertion_sort([4, 6, 1, 3, 5, 2]))
</pre>
