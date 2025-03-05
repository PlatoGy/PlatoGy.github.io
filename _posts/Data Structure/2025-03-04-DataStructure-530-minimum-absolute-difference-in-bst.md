---
layout: post
title: 530-minimum-absolute-difference-in-bst
author: Patrick Gao
date: 2025-3-4 21:20
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
Given the root of a Binary Search Tree (BST), return the minimum absolute difference between the values of any two different nodes in the tree.

 

Example 1:


Input: root = [4,2,6,1,3]
Output: 1
Example 2:


Input: root = [1,0,48,null,null,12,49]
Output: 1
### My solution：
```python

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def __init__(self):
        self.arr = []
    def extract(self,root):
        if not root:
            return
        if root.left:
            self.extract(root.left)

        self.arr.append(root.val)

        if root.right:
            self.extract(root.right)
    def getMinimumDifference(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        res = float('inf')
        self.extract(root)
        for i in range(len(self.arr)-1):
            res = min(res,self.arr[i+1]-self.arr[i])
        return res
```
        