---
layout: post
title: 1-two-sum
author: Patrick Gao
date: 2025-01-31 22:41
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Hash Map
mermaid: true
math: true
pin: false
---

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]



### My first solution：

Use double for loop to calculate the target
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i] + nums[j] == target:
                    return [i,j]

```
Time Complexity: O(n**2)
Space Complexity: O(1)

### Best Solution

First of all, let me emphasize when to use the hash method, when we need to check whether an element has appeared, or whether an element is in the set, we should first think of the hash method. 

In this case, I'm going to need a set of elements that we've traversed, and then I'm going to ask that set, as I'm traversing the set, whether that element has traversed, that is, whether it appears in that set. Then we should think about using hashing.
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        visited = {}
        for index, val in enumerate(nums):
            # find the 
            if target - val in visited:
                return [visited[target - val], index]
            else:
              # store val as the key， store index as the value
                visited[val] = index

```