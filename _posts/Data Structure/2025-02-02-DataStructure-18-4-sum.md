---
layout: post
title: 18-4Sum
author: Patrick Gao
date: 2025-2-2 16:52
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Hash Map
  - Double pointer
mermaid: true
math: true
pin: false
---
Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

0 <= a, b, c, d < n
a, b, c, and d are distinct.
nums[a] + nums[b] + nums[c] + nums[d] == target
You may return the answer in any order.

 

Example 1:

Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
Example 2:

Input: nums = [2,2,2,2,2], target = 8
Output: [[2,2,2,2]]




### My first solution：
It's similar with 3 sum, but use 2 for-loops, 
```python
class Solution(object):
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        res = []
        nums = sorted(nums)
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                left = j + 1
                right = len(nums) - 1
                while left < right:
                    quadruplets = nums[i] + nums[j] + nums[left] + nums[right]
                    if quadruplets < target:
                        left += 1
                    elif quadruplets > target:
                        right -= 1
                    else:
                        unique = [nums[i], nums[j], nums[left], nums[right]]
                        # cut branches
                        if unique not in res:
                            res.append([nums[i], nums[j], nums[left], nums[right]])
                        while left < right and nums[left] == nums[left+1]:
                            left += 1
                        while left < right and nums[right] == nums[right-1]:
                            right -= 1
                        left += 1
                        right -= 1
                    
        return res


Time Complexity: O(n**3)
Space Complexity: O(1)

Thought reference link: [https://programmercarl.com](https://programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E6%80%9D%E8%B7%AF)