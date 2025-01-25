---
layout: post
title: 27 Move Element
author: Patrick Gao
date: 2025-01-27 21:19
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Array
  - fast and slow pointer
mermaid: true
math: true
pin: false
---

# 27 Move Element

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
Return k.


```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        # use a fast and a slow index to move
        slowIndex, fastIndex = 0, 0
        while fastIndex < len(nums):
            # when fastval == val, move fastIndex; else exchange value and move both
            if nums[fastIndex] != val:
                nums[slowIndex] = nums[fastIndex]
                slowIndex += 1
            fastIndex += 1
        return slowIndex

```



Time Complexity: `O(n)`

Space Complexity: `O(1)`