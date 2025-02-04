---
layout: post
title: 20-valid-parentheses
author: Patrick Gao
date: 2025-2-4 03:21
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Quene and Stack
mermaid: true
math: true
pin: false
---
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
 

Example 1:

Input: s = "()"

Output: true

Example 2:

Input: s = "()[]{}"

Output: true

Example 3:

Input: s = "(]"

Output: false

Example 4:

Input: s = "([])"

Output: true

### My solution：
```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        for el in s:
            if el == '(' or el == '[' or el == '{':
                stack.append(el)
            else:
                if len(stack) == 0:
                    return False
                if el == ')' and stack.pop() != '(':
                    return False
                elif el == ']' and stack.pop() != '[':
                    return False
                elif el == '}' and stack.pop() != '{':
                    return False
        return True if len(stack) == 0 else False

```

Time Complexity: O(n)
Space Complexity: O(n)