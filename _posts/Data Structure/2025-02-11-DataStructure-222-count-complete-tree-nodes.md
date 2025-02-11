---
layout: post
title: 222-count-complete-tree-nodes
author: Patrick Gao
date: 2025-2-11 01:44
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
mermaid: true
math: true
pin: false
---
Given the root of a complete binary tree, return the number of the nodes in the tree.

According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

Design an algorithm that runs in less than O(n) time complexity.

 

Example 1:


Input: root = [1,2,3,4,5,6]
Output: 6
Example 2:

Input: root = []
Output: 0
Example 3:

Input: root = [1]



### Recursion solution：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution(object):
    def countNodes(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        return self.count(root)    
    def count(self,root):
        if not root:
            return 0
        leftCount = self.count(root.left)
        rightCount = self.count(root.right)
        sumCount = leftCount + rightCount + 1
        return sumCount
        
```

### Iteration solution(Use Stack)：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution(object):
    def countNodes(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        count = 0
        if not root:
            return count
        queue = deque()
        queue.append(root)
        while queue:
            length = len(queue)
            for i in range(length):
                cur = queue.popleft()
                count += 1
                if cur.right:
                    queue.append(cur.right)
                    queue.append(cur.left)
                elif cur.left:
                    queue.append(cur.left)
        return count                    

```