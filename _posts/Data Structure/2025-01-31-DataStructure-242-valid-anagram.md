---
layout: post
title: 242-valid-anagram
author: Patrick Gao
date: 2025-01-31 21:00
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Hash Map
mermaid: true
math: true
pin: false
---
Given two strings s and t, return true if t is an 
anagram
 of s, and false otherwise.

 

Example 1:

Input: s = "anagram", t = "nagaram"

Output: true

Example 2:

Input: s = "rat", t = "car"

Output: false
 


My solution：

Use dict data structure to count the occurence of every character of s, and then minus them when they occur in t.
```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        if len(s) != len(t):
            return False
        visited = {}
        for char in s:
            if char in visited:
                visited[char] += 1
            else:
                visited[char] = 1
        
        for char in t:
            if char in visited:
                visited[char] -= 1

        for char in visited:
            if visited[char] != 0:
                return False
                
        return True       
        
```

Time Complexity: O(n)
Space Complexity: O(n)