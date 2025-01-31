---
layout: post
title: 349-intersection-of-two-arrays
author: Patrick Gao
date: 2025-01-31 22:00
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Hash Map
mermaid: true
math: true
pin: false
---

Given two integer arrays nums1 and nums2, return an array of their 
intersection
. Each element in the result must be unique and you may return the result in any order.

 

Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
Example 2:

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.

My solution：

Use dict data structure to count the occurence of every character of s, and then minus them when they occur in t.
```python
class Solution(object):
    def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        shortSet = set(nums2) if len(nums1) > len(nums2) else set(nums1)
        longSet = set(nums2) if len(nums1) <= len(nums2) else set(nums1)

        intersectionArr = []
        for el in shortSet:
            if el in longSet:
                intersectionArr.append(el)
        return intersectionArr
```

Time Complexity: O(n)
Space Complexity: O(n)