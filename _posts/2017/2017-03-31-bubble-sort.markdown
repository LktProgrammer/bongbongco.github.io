---
layout: post
title: 버블정렬(Bubble Sort)
categories: [Programming]
tags: [Programming, Algorithm]
fullview: false
comments: true
published: true
use_math: false
---

인접한 두개의 원소를 비교하여 자리를 교환하는 방식으로, 첫 번째 원소부터 마지막 원소까지 반복하면 가장 큰 원소가 마지막 자리로 정렬하게 된다. 첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 마지막 자리로 이동하는 모습이 물 속에서 물위로 올라오는 물방울 모양과 같다고 해서 버블 정렬이라고 한다.


<pre class="lang:default decode:true " >
import unittest

def bubblesort(alist):
  for i in range(len(alist) -1):
    for j in range(len(alist) -1):
      if alist[j] &gt; alist[j+1]:
        alist[j], alist[j+1] = alist[j+1], alist[j]
  return alist

class unit_test(unit test, TestCase)
  def test(self):
    self.assertEqual([1, 2, 3, 4, 5, 6], bubblesort([4, 6, 1, 3, 5, 2,]))</pre> 
