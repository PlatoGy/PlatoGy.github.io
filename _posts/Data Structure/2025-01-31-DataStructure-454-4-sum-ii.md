---
layout: post
title: 454-4-sum-ii
author: Patrick Gao
date: 2025-2-1 01:13
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Hash Map
mermaid: true
math: true
pin: false
---
Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, return the number of tuples (i, j, k, l) such that:

0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
 

Example 1:

Input: nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
Output: 2
Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
Example 2:

Input: nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
Output: 1




### My first solution：

Use double for loop to calculate the target
```python
class Solution(object):
    def fourSumCount(self, nums1, nums2, nums3, nums4):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :type nums3: List[int]
        :type nums4: List[int]
        :rtype: int
        """
        # combine nums1&nums2,nums3&nums4
        dict1 = {}
        dict2 = {}
        for i,el1 in enumerate(nums1):
            for j,el2 in enumerate(nums2):
                if el1+el2 in dict1:
                    dict1[el1+el2] += 1
                else:
                    dict1[el1+el2] = 1

        
        for i,el1 in enumerate(nums3):
            for j,el2 in enumerate(nums4):
                if el1+el2 in dict2:
                    dict2[el1+el2] += 1
                else:
                    dict2[el1+el2] = 1
        count = 0
        
        for key1,val1 in dict1.items():
            for key2,val2 in dict2.items():
                if key1 + key2 == 0:
                    # if sum == 0, mutiply the val1 and val2
                    count += val1 * val2
        return count

```
Time Complexity: O(n**2)
Space Complexity: O(n**2)

### Best Solution
The same thought as mine, but no need to have the third for loop, just count the number in the second loop.

```python
class Solution(object):
    def fourSumCount(self, nums1, nums2, nums3, nums4):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :type nums3: List[int]
        :type nums4: List[int]
        :rtype: int
        """
        dict1 = {}
        for i,el1 in enumerate(nums1):
            for j,el2 in enumerate(nums2):
                if el1+el2 in dict1:
                    dict1[el1+el2] += 1
                else:
                    dict1[el1+el2] = 1

        count = 0
        for i,el1 in enumerate(nums3):
            for j,el2 in enumerate(nums4):
                # because the sum is 0
                sumVal = -el1 - el2
                if sumVal in dict1:
                    count += dict1[sumVal]

        return count

```