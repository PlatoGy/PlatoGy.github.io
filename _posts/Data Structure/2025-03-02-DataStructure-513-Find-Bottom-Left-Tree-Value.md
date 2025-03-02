---
layout: post
title: 513-Find Bottom Left Tree Value
author: Patrick Gao
date: 2025-3-2 21:37
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
  - Recursion
mermaid: true
math: true
pin: false
---
513. Find Bottom Left Tree Value
Solved
Medium
Topics
Companies
Given the root of a binary tree, return the leftmost value in the last row of the tree.
 

Example 1:


Input: root = [2,1,3]
Output: 1
Example 2:


Input: root = [1,2,3,4,null,5,6,null,null,7]
Output: 7

### My solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution(object):
    def findBottomLeftValue(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        
        queue = deque()
        queue.append(root)
        leftMostTmp = None
        while queue:
            length = len(queue)
            leftMostTmp = queue.popleft()
            if leftMostTmp.left:
                    queue.append(leftMostTmp.left)
            if leftMostTmp.right:
                queue.append(leftMostTmp.right)

            for i in range(1,length):
                tmp = queue.popleft()
                if tmp.left:
                    queue.append(tmp.left)
                if tmp.right:
                    queue.append(tmp.right)

        return leftMostTmp.val
```
  
