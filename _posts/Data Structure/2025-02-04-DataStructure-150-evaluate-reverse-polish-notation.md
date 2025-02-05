---
layout: post
title: 150-evaluate-reverse-polish-notation
author: Patrick Gao
date: 2025-2-4 11:59
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Stack and Quene
mermaid: true
math: true
pin: false
---
You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

The valid operators are '+', '-', '*', and '/'.
Each operand may be an integer or another expression.
The division between two integers always truncates toward zero.
There will not be any division by zero.
The input represents a valid arithmetic expression in a reverse polish notation.
The answer and all the intermediate calculations can be represented in a 32-bit integer.
 

Example 1:

Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
Example 2:

Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
Example 3:

Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22






### My solution：
class Solution(object):
    def evalRPN(self, tokens):
        """
        :type tokens: List[str]
        :rtype: int
        """
        stack = []
        for token in tokens:
            if token == '+' or token == '-' or token == '*' or token == '/':
                a = int(stack.pop())
                b = int(stack.pop())
                res = 0
                if token == '+':
                    res = a + b
                    stack.append(res)
                elif token == '*':
                    res = a * b
                    stack.append(res)
                elif token == '/':
                    # truncates toward zero
                    if b % a == 0:
                        res =  b / a
                    else: 
                        res =  b // a if a * b >= 0 else b // a + 1
                    stack.append(res)
                elif token == '-':
                    res = b - a
                    stack.append(res)
            else:
                stack.append(token)  
        return int(stack[0])    
        

Time Complexity: O(n)
Space Complexity: O(n)

### Best solution：
