---
layout: post
title: 26 remove-duplicates-from-sorted-array
author: Patrick Gao
date: 2025-01-26 15:25
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

# 26 remove-duplicates-from-sorted-array

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.


```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # if length of nums is only 1
        if len(nums) == 1:
            return 1
        
        fastIndex, slowIndex = 1, 0
        while fastIndex < len(nums):
            # if fast is same as slow, fast moves; else, slow moves and gets value of fast;
            if(nums[fastIndex] != nums[slowIndex]):
                slowIndex += 1
                nums[slowIndex] = nums[fastIndex]
            fastIndex += 1
            
        # finally get 1 more than slowIndex    
        return slowIndex+1

```



Time Complexity: `O(n)`

Space Complexity: `O(1)`