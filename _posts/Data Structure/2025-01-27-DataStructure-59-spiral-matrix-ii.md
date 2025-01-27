---
layout: post
title: 59 spiral-matrix-ii
author: Patrick Gao
date: 2025-01-27 11:32
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Array
mermaid: true
math: true
pin: false
---

# 59 spiral-matrix-ii

Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

Example 1:

Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
Example 2:

Input: n = 1
Output: [[1]]


My solution：
It's not a difficult question, but it is complicated.

```python
class Solution(object):

    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        # a function to generate the length of every step
        def get_length(n):
            arr = [float('inf')] * (2*n -1)
            arr[0] = n
            arr[-1] = 1
            arr[-2] = 1
            num = n-1
            i = 1
            while(i < 2*n-3):
                count = 0
                while(count<2):
                    count += 1
                    arr[i] = num
                    i += 1 
                num -= 1
            return arr[::-1]

        # Special condition, when n is only 1
        if n == 1:
            return [[1]]

        # Initialize the matrix n * n
        matrix = [[float('inf') for _ in range(n)] for _ in range(n)]
        num = 1
        steps = 2*n - 1 # steps is the counter of movement 
        length = 0 # length is the moving distance each time
        direction = 0 # use for judge direction, 0 -> left, 1 -> down, 2 -> up, 3 -> right
        length_arr = get_length(n) # store length of every step
        i = 0 # index 
        j = 0 # index 
        while steps:
            length = length_arr[steps-1]
            if direction % 4 == 0:
                step_part = 0
                while step_part < length:
                    matrix[i][j] = num
                    j += 1
                    num += 1
                    step_part += 1
                j -= 1
                i += 1
            elif direction % 4 == 1:
                step_part = 0
                while step_part < length:
                    matrix[i][j] = num
                    i += 1
                    num += 1
                    step_part += 1
                i -= 1
                j -= 1
            elif direction % 4 == 2:
                step_part = 0
                while step_part < length:
                    matrix[i][j] = num
                    j -= 1
                    num += 1
                    step_part += 1
                j += 1
                i -= 1
            else:
                step_part = 0
                while step_part < length:
                    matrix[i][j] = num
                    i -= 1
                    num += 1
                    step_part += 1
                i += 1
                j += 1
            direction += 1
            steps -= 1
        return matrix
        

```

Time Complexity: `O(n)`

Space Complexity: `O(1)`

Best Solution
```python
class Solution(object):
    def sortedSquares(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = []
        left, right = 0, len(nums) - 1
        while left <= right :
            if abs(nums[left]) > abs(nums[right]):
                res.insert(0,nums[left]**2)
                left += 1
            else:
                res.insert(0,nums[right]**2)
                right -= 1
        return res
        
```

Time Complexity: `O(n^2)`