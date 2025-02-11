---
layout: post
title: 104-maximum-depth-of-binary-tree
author: Patrick Gao
date: 2025-2-10 20:51
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
mermaid: true
math: true
pin: false
---
[代码随想录详细解析](https://programmercarl.com/0104.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

 

Example 1:


Input: root = [3,9,20,null,null,15,7]
Output: 3
Example 2:

Input: root = [1,null,2]
Output: 2


### My solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        if not root:
            return 0
        depth = 0
        queue = deque()
        queue.append(root)
        while queue:
            length = len(queue)
            if length:
                depth += 1
            for i in range(length):
                cur = queue.popleft()
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
        return depth
```
        
### recursion solution:
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        return self.getHeight(root)
        
    def getHeight(self,root):
        if not root:
            return 0
        leftHeight = self.getHeight(root.left)
        rightHeight = self.getHeight(root.right)
        return 1 + max(leftHeight,rightHeight)
```