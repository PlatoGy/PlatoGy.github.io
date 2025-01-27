---
layout: post
title: 203-remove-linked-list-elements
author: Patrick Gao
date: 2025-01-27 16:31
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Linked List
mermaid: true
math: true
pin: false
---

Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]
Example 2:

Input: head = [], val = 1
Output: []
Example 3:

Input: head = [7,7,7,7], val = 7
Output: []



My solution：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: Optional[ListNode]
        :type val: int
        :rtype: Optional[ListNode]
        """
        # virtual head
        dummyhead = ListNode(val=0,next=head)
        curr = dummyhead 
        while curr.next:
            if curr.next.val == val:
                curr.next = curr.next.next
            else:
                curr = curr.next
        # dummyhead.next is the actural head
        return dummyhead.next
        
        
```
Time Complexity: `O(n)`
Space Complexity: `O(1)`
