---
layout: post
title: 101-symmetric-tree
author: Patrick Gao
date: 2025-2-11 00:53
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
mermaid: true
math: true
pin: false
---
Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

Example 1:


Input: root = [1,2,2,3,4,4,3]
Output: true
Example 2:


Input: root = [1,2,2,null,3,null,3]
Output: false



### Recursion solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        return self.isSym(root.left,root.right)

    def isSym(self,left,right):
        if not left and right:
            return False
        elif not right and left:
            return False
        elif not left and not right:
            return True
        elif left.val != right.val:
            return False
        outside = self.isSym(left.left,right.right)
        inside = self.isSym(left.right,right.left)
        if outside and inside:
            return True
        else:
            return False
        
```

### Iteration solution(Use Stack)：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        stack = [root.left,root.right]
        while stack:
            right = stack.pop()
            left = stack.pop()
            if not right and left:
                return False
            elif not left and right:
                return False
            elif not right and not left:
                continue
            elif right.val != left.val:
                return False
            
            stack.append(right.right)
            stack.append(left.left)
            stack.append(left.right)
            stack.append(right.left)
        
        return True



```