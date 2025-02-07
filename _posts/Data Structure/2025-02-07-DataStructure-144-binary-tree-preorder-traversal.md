---
layout: post
title: 144-binary-tree-preorder-traversal
author: Patrick Gao
date: 2025-2-7 13:53
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

Given the root of a binary tree, return the preorder traversal of its nodes' values.

 

Example 1:

Input: root = [1,null,2,3]

Output: [1,2,3]

Explanation:



Example 2:

Input: root = [1,2,3,4,5,null,8,null,null,6,7,9]

Output: [1,2,4,5,6,7,3,8,9]

Explanation:



Example 3:

Input: root = []

Output: []

Example 4:

Input: root = [1]

Output: [1] 





### Recursion solution：

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[int]
        """
        res = []
        def dfs(parent):
            if not parent:
                return
            res.append(parent.val)
            dfs(parent.left)
            dfs(parent.right)

        dfs(root)
        return res
        
```

### Iteration solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[int]
        """
        res = []
        if not root: 
            return res

        stack = [root]
        while stack:
            tmp = stack.pop()
            res.append(tmp.val)
            # preorder is mid -> left -> right, so we append right firstly because this could make left out of stack advance.
            if tmp.right:
                stack.append(tmp.right)
            if tmp.left:
                stack.append(tmp.left)


        return res

```

