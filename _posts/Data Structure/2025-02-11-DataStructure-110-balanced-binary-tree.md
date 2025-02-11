---
layout: post
title: 110-balanced-binary-tree
author: Patrick Gao
date: 2025-2-11 13:44
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
mermaid: true
math: true
pin: false
---
Given a binary tree, determine if it is height-balanced.
 
Example 1:

Input: root = [3,9,20,null,null,15,7]
Output: true
Example 2:

Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
Example 3:

Input: root = []
Output: true

### My solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        return True if self.getHeight(root) != -1 else False
    # recursion function
    # step1: parameter
    def getHeight(self,root):
        # step2: stop condition
        if not root:
            return 0
        # step3: operation on every recursion 
        leftHeight = self.getHeight(root.left)
        rightHeight = self.getHeight(root.right)
        if abs(leftHeight - self.getHeight(root.right)) > 1:
            return -1
        elif leftHeight == -1 or rightHeight == -1:
            return -1
        else:
            return max(leftHeight,rightHeight) + 1
```      
        

