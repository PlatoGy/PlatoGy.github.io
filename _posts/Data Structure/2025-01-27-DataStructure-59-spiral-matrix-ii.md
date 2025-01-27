---
layout: post
title: 58 length-of-last-word
author: Patrick Gao
date: 2025-01-27 11:32
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - String
mermaid: true
math: true
pin: false
---

# 58 length-of-last-word

Given a string s consisting of words and spaces, return the length of the last word in the string.

A word is a maximal 
substring
 consisting of non-space characters only.

 

Example 1:

Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
Example 2:

Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
Example 3:

Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.

```python
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        # cut the space and reverse the string
        s = s.strip()[::-1]
        res = 0
        for i in s:
            if i != ' ':
                res += 1
            else:
                break
        return res
```

Time Complexity: `O(n)`
Space Complexity: `O(1)`
