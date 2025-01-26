---
layout: post
title: 209 minimum-size-subarray-sum
author: Patrick Gao
date: 2025-01-24 16:57
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Array
  - sliding window
mermaid: true
math: true
pin: false
---

# 209 minimum-size-subarray-sum

Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray
 whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

 

Example 1:

Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
Example 2:

Input: target = 4, nums = [1,4,4]
Output: 1
Example 3:

Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0


wrong answer:
Firstly, I use sorted to sort the nums, but this is not allowed by the description of subarray:
```python
class Solution(object):
    def minSubArrayLen(self, target, nums):
        """
        :type target: int
        :type nums: List[int]
        :rtype: int
        """
        sort_nums = sorted(nums, reverse=True)
        i = 0
        sum = 0
        while i < len(nums):
            sum += sort_nums[i]
            print(i,sum)
            if sum >= target:
                return (i + 1)
            i += 1
        return 0
```

Then I use 2 loop to violently solve it, apparently the result is over time.

```python
class Solution(object):
    def minSubArrayLen(self, target, nums):
        """
        :type target: int
        :type nums: List[int]
        :rtype: int
        """
        i = 0
        res = 0
        if sum(nums) >= target:
            res = len(nums)
        else:
            return 0
        while i < len(nums):
            j = i
            while j < len(nums):
                if sum(nums[i:j+1]) >= target:
                    res = min(res,j-i+1)
                j += 1
            i += 1
        return res

```

Time Complexity: `O(n^2)`
Space Complexity: `O(1)`

Best solution:
```python
class Solution(object):
    def minSubArrayLen(self, target, nums):
        """
        :type target: int
        :type nums: List[int]
        :rtype: int
        """
        left = 0
        right = 0
        # sum value between left and right
        sum_val = 0
        window = float('inf')
        while right < len(nums):
            sum_val += nums[right]
            
            # if sum_val >= target, move left pointer until sum_val < target
            while sum_val >= target:
                # reduce window
                window = min(window, right - left + 1)
                sum_val -= nums[left]
                left += 1

            right += 1
        # if window is still infinity, return 0
        return window if window != float('inf') else 0
```
Time Complexity: `O(n)`
Space Complexity: `O(1)`
