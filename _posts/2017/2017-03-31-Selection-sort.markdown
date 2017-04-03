---
layout: post
title: 선택정렬(Selection Sort)
categories: [Programming]
tags: [Programming, Algorithm]
fullview: false
comments: true
published: true
use_math: false
---


전체 원소들 중에서 기준 위치에 맞는 원소를 선택하여 자리를 교환하는 방식으로 정렬한다. 전체 원소 중에서 가장 작은 원소를 찾아서 선택하고 첫 번째 원소와 자리를 교환한다. 그 다음 두 번째로 작은 원소를 찾아 선택하여 두 번째 원소와 자리를 교환하고, 그 다음에는 세 번째로 작은 원소를 찾아서 세 번째 원소와 자리를 교환한다. 이 과정을 반복하면서 정렬을 완성한다.

비교 횟수를 따져보면 첫 번째 맞바꿀 때는 n-1 번, 그 다음에는 n-2번, 그 다음에는 n-3번 같은 식이 된다. 따라서 총 비교 횟수는 (n-1)+(n-2)+...+1 이므로 n(n-1)/2 임을 알 수 있다. 따라서 이 알고리즘은 최선, 평균, 최악의 경우 모두 O(n^2)이다. 처음 시작할 때의 정렬 상태는 비교 횟수에는 전혀 영향을 미치지 않는다.
<pre class="lang:python decode:true ">
import unittest

def selectionSort(input):
  for i in range(len(input) - 1):
    idx_min = i
    j = i + 1

    while j < len(input):
      if(input[j] < input[idx_min]):
        idx_min = j
      j = j + 1

    if idx_min is not i:
      input[idx_min], input[i] = input[i], input[idx_min]

  return input

class unit_test(unittest.TestCase):
  def test(self):
    self.assertEqual([1, 2, 3, 4, 5, 6], selectionSort([4, 6, 1, 3, 5, 2]))
</pre>
