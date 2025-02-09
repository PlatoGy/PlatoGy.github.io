---
layout: post
title: 102-binary-tree-level-order-traversal
author: Patrick Gao
date: 2025-2-9 20:56
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
Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).
 

Example 1:


Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
Example 2:

Input: root = [1]
Output: [[1]]
Example 3:

Input: root = []
Output: []



### My solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[List[int]]
        """
        if not root:
            return []
        stack = [root]
        res = []
        while stack:
            tmp = []
            val = []
            while stack:
                cur = stack.pop(0)
                val.append(cur.val)
                if cur.left:
                    tmp.append(cur.left)
                if cur.right:
                    tmp.append(cur.right)
            stack = tmp[:]
            res.append(val)
        return res
            
```
        
