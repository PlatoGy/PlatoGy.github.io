---
layout: post
title: 501-find-mode-in-binary-search-tree
author: Patrick Gao
date: 2025-3-5 00:41
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
Given the root of a binary search tree (BST) with duplicates, return all the mode(s) (i.e., the most frequently occurred element) in it.

If the tree has more than one mode, return them in any order.

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than or equal to the node's key.
The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
Both the left and right subtrees must also be binary search trees.
 

Example 1:


Input: root = [1,null,2,2]
Output: [2]
Example 2:

Input: root = [0]
Output: [0]

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
        self.set = {}
    
    def extract(self,root):
        if not root:
            return
        if root.left:
            self.extract(root.left)
        if root.val in self.set:
            self.set[root.val] += 1
        else:
            self.set[root.val] = 1
        if root.right:
            self.extract(root.right)

    def findMode(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[int]
        """
        self.extract(root)
        maximum = max(self.set.values())
        res = []
        for key,value in self.set.items():
            if value == maximum:
                res.append(key)
        return res
```
        