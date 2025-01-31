---
layout: post
title: 202-happy-number
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

Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:

Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.
Return true if n is a happy number, and false if not.
 

Example 1:

Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
Example 2:

Input: n = 2
Output: false


My solution：

Use dict data structure to count the occurence of every character of s, and then minus them when they occur in t.
```python
class Solution(object):
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        NumSet = set()
        nStr = str(n)
        while nStr not in NumSet:
            NumSet.add(nStr)
            # calculation
            nAdd = sum([int(num)**2 for num in nStr])
            nStr = str(nAdd)
            if nStr == '1':
                return True
        return False
```
