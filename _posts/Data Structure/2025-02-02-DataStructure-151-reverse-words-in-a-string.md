---
layout: post
title: 151-reverse-words-in-a-string
author: Patrick Gao
date: 2025-2-2 18:20
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - String
mermaid: true
math: true
pin: false
---
Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

 

Example 1:

Input: s = "the sky is blue"
Output: "blue is sky the"
Example 2:

Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
Example 3:

Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.




### My solution：

```python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        s = s.strip()
        arr = []
        i,j = 0,0
        while j < len(s):
            while j < len(s) and s[j] != ' ':
                j += 1
            arr.append(s[i:j])
            while j < len(s) and s[j] == ' ' :
                j += 1
            i = j

        return ' '.join(arr[::-1])


Time Complexity: O(n)
Space Complexity: O(1)
