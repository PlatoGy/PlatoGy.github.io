---
layout: post
title: 199-binary-tree-right-side-view
author: Patrick Gao
date: 2025-2-9 22:14
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
mermaid: true
math: true
pin: false
---
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

 

Example 1:

Input: root = [1,2,3,null,5,null,4]

Output: [1,3,4]

Explanation:



Example 2:

Input: root = [1,2,3,4,null,null,null,5]

Output: [1,3,4,5]

Explanation:



Example 3:

Input: root = [1,null,3]

Output: [1,3]

Example 4:

Input: root = []

Output: []
Output: []



### My solution：
```python
from collections import deque
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def rightSideView(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[int]
        """
        if not root:
            return []
        quene = deque()
        quene.append(root)
        res = []
        while quene:
            length = len(quene)
            res.append(quene[-1].val)
            for i in range(length):
                cur = quene.popleft()
                if cur.left:
                    quene.append(cur.left)
                if cur.right:
                    quene.append(cur.right)
        return res
```
        
