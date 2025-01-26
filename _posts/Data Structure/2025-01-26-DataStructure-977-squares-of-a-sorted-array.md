---
layout: post
title: 977 squares-of-a-sorted-array
author: Patrick Gao
date: 2025-01-24 15:49
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Array
  - double pointer
mermaid: true
math: true
pin: false
---

# 977 squares-of-a-sorted-array

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

 

Example 1:

Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
Example 2:

Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]



```python
class Solution(object):
    def sortedSquares(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        # init res list for length of nums, each value is infinity
        res = [float('inf')] * len(nums)
        # i is the index of res
        left, right, i = 0, len(nums) - 1, len(nums) - 1
        while left <= right :
            if abs(nums[left]) > abs(nums[right]):
                res[i] = nums[left]**2
                i -= 1
                left += 1
            else:
                res[i] = nums[right]**2
                i -= 1
                right -= 1
        return res
        

```

Time Complexity: `O(n)`

Space Complexity: `O(1)`


Firstly, I use the same method as I use in Javascript, but it would use more time because the Time Complexity of insert is O(n):
```python
class Solution(object):
    def sortedSquares(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = []
        left, right = 0, len(nums) - 1
        while left <= right :
            if abs(nums[left]) > abs(nums[right]):
                res.insert(0,nums[left]**2)
                left += 1
            else:
                res.insert(0,nums[right]**2)
                right -= 1
        return res
        
```

Time Complexity: `O(n^2)`