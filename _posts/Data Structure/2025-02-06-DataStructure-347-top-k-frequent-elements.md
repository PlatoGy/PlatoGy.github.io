---
layout: post
title: 347-top-k-frequent-elements
author: Patrick Gao
date: 2025-2-6 19:20
categories:
  - Data Struture
  - LeetCode Exercise
tags:
mermaid: true
math: true
pin: false
---

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

 

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Example 2:

Input: nums = [1], k = 1
Output: [1]





### My solution：
```python
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        count = {}
        for num in nums:
            if num in count:
                count[num] += 1
            else:
                count[num] = 1

        res = []
        countQuene = sorted(count.values())[-k:]
        for key,value in count.items():
            if value in countQuene:
                res.append(key)

        return res
            
```
        

Time Complexity: O(n)
Space Complexity: O(n)

