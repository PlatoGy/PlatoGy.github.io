---
layout: post
title: 383-ransom-note
author: Patrick Gao
date: 2025-2-1 20:54
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Hash Map
mermaid: true
math: true
pin: false
---
Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.

Each letter in magazine can only be used once in ransomNote.

 

Example 1:

Input: ransomNote = "a", magazine = "b"
Output: false
Example 2:

Input: ransomNote = "aa", magazine = "ab"
Output: false
Example 3:

Input: ransomNote = "aa", magazine = "aab"
Output: true




### My first solution：

```python
class Solution(object):
    def canConstruct(self, ransomNote, magazine):
        """
        :type ransomNote: str
        :type magazine: str
        :rtype: bool
        """
        magDict = {}
        for char in magazine:
            if char in magDict:
                magDict[char] += 1
            else:
                magDict[char] = 1

        for char in ransomNote:
            if char not in magDict or magDict[char] == 0:
                return False
            else:
                magDict[char] -= 1
                
        return True

```
Time Complexity: O(n)
Space Complexity: O(1)

### Best Solution
Similar with mine, but use list rather than dict because this can save space.

```python
class Solution(object):
    def canConstruct(self, ransomNote, magazine):
        """
        :type ransomNote: str
        :type magazine: str
        :rtype: bool
        """
        if len(magazine) < len(ransomNote):
            return False
        magList = [0]*26
        for char in magazine:
            magList[ord(char) - ord('a')] += 1

        for char in ransomNote:
            if magList[ord(char) - ord('a')] == 0:
                return False
            else:
                magList[ord(char) - ord('a')] -= 1

        return True

```
Time Complexity: O(n)
Space Complexity: O(1)