---
layout: post
title: 257-binary-tree-paths
author: Patrick Gao
date: 2025-2-12 15:20
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
Given the root of a binary tree, return all root-to-leaf paths in any order.

A leaf is a node with no children.

 

Example 1:


Input: root = [1,2,3,null,5]
Output: ["1->2->5","1->3"]
Example 2:

Input: root = [1]
Output: ["1"]


## Recursion
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def binaryTreePaths(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[str]
        """
        path = str(root.val)
        res = []
        self.getPaths(root,res,path)
        return res

    def getPaths(self,root,res,path):
        if not root.left and not root.right:
            res.append(path)
            return
        if root.left:
            pathLeft = path + '->' + str(root.left.val)
            self.getPaths(root.left,res,pathLeft)
        if root.right:
            pathRight = path + '->' + str(root.right.val)
            self.getPaths(root.right,res,pathRight)
        
```        
