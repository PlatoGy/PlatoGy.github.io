---
layout: post
title: 541-reverse-string-ii
author: Patrick Gao
date: 2025-2-2 17:20
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - String
mermaid: true
math: true
pin: false
---
Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

 

Example 1:

Input: s = "abcdefg", k = 2
Output: "bacdfeg"
Example 2:

Input: s = "abcd", k = 2
Output: "bacd"




### My solution：

```python
class Solution(object):
    def reverseStr(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: str
        """
        i = 0
        length = len(s)
        while i < length:
            s = s[:i] + s[i:i+k][::-1] + s[i+k:]
            i += 2*k
        return s


Time Complexity: O(n)
Space Complexity: O(1)
