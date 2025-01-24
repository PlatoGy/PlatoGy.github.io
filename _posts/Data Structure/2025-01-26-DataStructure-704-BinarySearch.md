---
layout: post
title: 704 Binary Search
author: Patrick Gao
date: 2025-01-24 21:48
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Array
  - binary search
mermaid: true
math: true
pin: false
---

# 704 Binary Search

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.



```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left = 0
        right = len(nums)-1
        while left <= right :
            # use (right - left)/2 to prevent overflow caused by a large value
            # '//' floor divide, get int value
            middle = left + (right -left) // 2 
            if nums[middle] > target:
                right = middle - 1
            elif nums[middle] < target:
                left = middle + 1
            else:
                return middle
        return -1

```



Time Complexity: `O(logn)`

Space Complexity: `O(1)`