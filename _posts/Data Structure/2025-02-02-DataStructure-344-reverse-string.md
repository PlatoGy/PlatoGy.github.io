---
layout: post
title: 344-reverse-string
author: Patrick Gao
date: 2025-2-2 17:00
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - String
mermaid: true
math: true
pin: false
---
Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

 

Example 1:

Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
Example 2:

Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]




### My first solution：

```python
class Solution(object):
    def reverseString(self, s):
        """
        :type s: List[str]
        :rtype: None Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s)-1
        while left < right:
            s[left],s[right] = s[right],s[left]
            left += 1
            right -= 1
        
        


Time Complexity: O(n)
Space Complexity: O(1)
