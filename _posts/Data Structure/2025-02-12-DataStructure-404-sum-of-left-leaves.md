---
layout: post
title: 404-sum-of-left-leaves
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
## Recursion
Given the root of a binary tree, return the sum of all left leaves.

A leaf is a node with no children. A left leaf is a leaf that is the left child of another node.

Example 1:

Input: root = [3,9,20,null,null,15,7]
Output: 24
Explanation: There are two left leaves in the binary tree, with values 9 and 15 respectively.
Example 2:

Input: root = [1]
Output: 0

### My solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def sumOfLeftLeaves(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        leftVals = []
        self.getSum(root,leftVals,False)
        return sum(leftVals)

    def getSum(self,root,leftVals,isLeft):
        if not root.left and not root.right and isLeft:
            leftVals.append(root.val)
            return
        if root.left:
            self.getSum(root.left,leftVals,True)
        if root.right:
            self.getSum(root.right,leftVals,False)
        
```

### Best solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def sumOfLeftLeaves(self, root): # 1. parameter is root node
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        # 2. stop condition
        if not root:
            return 0
        if not root.left and not root.right:
            return 0
        
        # 3. every step operation  
        # postorder left -> right -> mid
        leftVal = self.sumOfLeftLeaves(root.left)
        rightVal = self.sumOfLeftLeaves(root.right)
        if root.left and not root.left.left and not root.left.right: # if the node is the left leaf
            leftVal = root.left.val
        return leftVal + rightVal
        
```