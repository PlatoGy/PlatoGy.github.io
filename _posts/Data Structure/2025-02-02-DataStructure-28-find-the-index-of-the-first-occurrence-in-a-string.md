---
layout: post
title: 28-find-the-index-of-the-first-occurrence-in-a-string
author: Patrick Gao
date: 2025-2-2 19:20
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - String
mermaid: true
math: true
pin: false
---
Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

 

Example 1:

Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
Example 2:

Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.




### My solution：
#### Use List.find()
```python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        return haystack.find(needle)
        

Time Complexity: O(n)
Space Complexity: O(1)
