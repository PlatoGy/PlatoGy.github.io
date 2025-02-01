---
layout: post
title: 15-3Sum
author: Patrick Gao
date: 2025-2-1 22:54
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
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

 

Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
Example 2:

Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
Example 3:

Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.





### My first solution：
Sadly the time limit is exceeded.
```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if (0 - nums[i] - nums[j]) in nums[j+1:]:
                    triplets = sorted([nums[i],nums[j],(0 - nums[i] - nums[j])])
                    if triplets not in res:
                        res.append(triplets)
        
        return res
        

```
Time Complexity: O(n**2)
Space Complexity: O(n)

### Best Solution
Similar with mine, but use list rather than dict because this can save space.

```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        nums = sorted(nums)
        # if the first number > 0 after sorted, all of the list > 0
        if nums[0] > 0:
            return res
        for i in range(len(nums)):
            # skip duplicate numbers
            if i > 0 and nums[i] == nums[i-1]:
                continue
            left = i + 1
            right = len(nums)-1
            while left < right:
                val = nums[i] + nums[left] + nums[right]
                if val < 0:
                    left += 1
                elif val > 0:
                    right -= 1
                else:
                    triplets = [nums[i], nums[left], nums[right]]
                    res.append(triplets)
                    # skip duplicate numbers
                    while right > left and nums[right] == nums[right - 1]:
                        right -= 1
                    while right > left and nums[left] == nums[left + 1]:
                        left += 1
                    left += 1
                    right -= 1

        return res

```
Time Complexity: O(n**2)
Space Complexity: O(1)

Thought reference link: [https://programmercarl.com](https://programmercarl.com/0015.%E4%B8%89%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E6%80%9D%E8%B7%AF)