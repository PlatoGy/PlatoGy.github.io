---
layout: post
title: 116-populating-next-right-pointers-in-each-node
author: Patrick Gao
date: 2025-2-10 16:21
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
mermaid: true
math: true
pin: false
---
You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

 

Example 1:


Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
Example 2:

Input: root = []
Output: []



### My solution：
```python
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
from collections import deque
class Solution(object):
    def connect(self, root):
        """
        :type root: Node
        :rtype: Node
        """
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
from collections import deque
class Solution(object):
    def connect(self, root):
        """
        :type root: Node
        :rtype: Node
        """
        if not root:
            return root
        queue = deque()
        queue.append(root)
        while queue:
            length = len(queue)
            for i in range(length):
                cur = queue.popleft()
                if i == length - 1:
                    cur.next = None
                else:
                    cur.next = queue[0]
                if cur.left:
                    queue.append(cur.left)
                    queue.append(cur.right)

        return root
```
        
