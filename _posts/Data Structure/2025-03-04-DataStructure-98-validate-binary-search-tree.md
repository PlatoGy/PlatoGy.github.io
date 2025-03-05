---
layout: post
title: 98-validate-binary-search-tree
author: Patrick Gao
date: 2025-3-4 21:20
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
  - Recursion
  - BST(Binary Search Tree)
mermaid: true
math: true
pin: false
---
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
 

Example 1:


Input: root = [2,1,3]
Output: true
Example 2:


Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.


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
    def isValidBST(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        if not root:
            return True
        
        self.extract(root)
        if sorted(self.arr) == self.arr and len(self.arr) == len(list(set(self.arr))):
            return True
        else:
            return False
        

```
        
