---
layout: post
title: 707-design-linked-list
author: Patrick Gao
date: 2025-01-29 23:44
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Linked List
mermaid: true
math: true
pin: false
---
Given the head of a singly linked list, reverse the list, and return the reversed list.

 

Example 1:


Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
Example 2:


Input: head = [1,2]
Output: [2,1]
Example 3:

Input: head = []
Output: []
 


 


My solution：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reverseList(self, head):
        """
        :type head: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        if not head:
            return head
        # use two temporary variable
        pre, curr = None, head
        while curr:
            # tmp to store the node not use
            tmp = curr.next
            curr.next = pre
            pre = curr
            curr = tmp
        return pre
```