---
layout: post
title: 617-Merge-Two-Binary-Trees
author: Patrick Gao
date: 2025-3-4 01:40
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

You are given two binary trees root1 and root2.

Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.

Return the merged tree.

Note: The merging process must start from the root nodes of both trees.

 

Example 1:


Input: root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
Output: [3,4,5,5,4,null,7]
Example 2:

Input: root1 = [1], root2 = [1,2]
Output: [2,2]





### My solution：
```python

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def mergeTrees(self, root1, root2):
        """
        :type root1: Optional[TreeNode]
        :type root2: Optional[TreeNode]
        :rtype: Optional[TreeNode]
        """
        left = None
        right = None

        if not root1 and not root2:
            return
        rootVal = 0
        if root1 and not root2:
            rootVal = root1.val
        elif root2 and not root1:
            rootVal = root2.val
        else:
            rootVal = root1.val + root2.val
            if not root1.left and not root2.left:
                left = None
            elif root1.left and not root2.left:
                left = root1.left
            elif root2.left and not root1.left:
                left = root2.left
            else:
                left = self.mergeTrees(root1.left,root2.left)
            
            if not root1.right and not root2.right:
                right = None
            elif root1.right and not root2.right:
                right = root1.right
            elif root2.right and not root1.right:
                right = root2.right
            else:
                right = self.mergeTrees(root1.right,root2.right)

        root = TreeNode(val=rootVal,left=left,right=right)
        return root
```
        

Time Complexity: 
Space Complexity: 

### Best solution：
