---
layout: post
title: 145-binary-tree-postorder-traversal
author: Patrick Gao
date: 2025-2-7 14:40
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
Given the root of a binary tree, return the postorder traversal of its nodes' values.

 

Example 1:

Input: root = [1,null,2,3]

Output: [3,2,1]

Explanation:



Example 2:

Input: root = [1,2,3,4,5,null,8,null,null,6,7,9]

Output: [4,6,7,5,2,9,8,3,1]

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
    def postorderTraversal(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[int]
        """
        res = []
        def dfs(parent):
            if not parent:
                return
            if parent.left:
                dfs(parent.left)
            if parent.right:
                dfs(parent.right)
            res.append(parent.val)
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
    def postorderTraversal(self, root):
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
            # firstly store parent to res
            res.append(tmp.val)
            # secondly store left to stack, so left enter res thirdly
            if tmp.left:
                stack.append(tmp.left)
            # thirdly store right, so right enter res secondly
            if tmp.right:
                stack.append(tmp.right)
        # reverse the res list, root <- right <- left
        return res[::-1]

        

```

