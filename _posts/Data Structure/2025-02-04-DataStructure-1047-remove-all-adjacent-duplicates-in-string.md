---
layout: post
title: 1047-remove-all-adjacent-duplicates-in-string
author: Patrick Gao
date: 2025-2-4 21:54
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Stack and Quene
mermaid: true
math: true
pin: false
---

You are given a string s consisting of lowercase English letters. A duplicate removal consists of choosing two adjacent and equal letters and removing them.

We repeatedly make duplicate removals on s until we no longer can.

Return the final string after all such duplicate removals have been made. It can be proven that the answer is unique.

 

Example 1:

Input: s = "abbaca"
Output: "ca"
Explanation: 
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
Example 2:

Input: s = "azxxzy"
Output: "ay"
 


### My solution：
class Solution(object):
    def removeDuplicates(self, s):
        """
        :type s: str
        :rtype: str
        """
        stack = []
        for el in s:
            if stack and stack[-1] == el:
                stack.pop()
            else:
                stack.append(el)
        return ''.join(stack)
        

Time Complexity: O(n)
Space Complexity: O(n)

