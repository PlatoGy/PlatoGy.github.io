---
layout: post
title: 24-swap-nodes-in-pairs
author: Patrick Gao
date: 2025-01-30 02:30
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Linked List
mermaid: true
math: true
pin: false
---
Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

 

Example 1:

Input: head = [1,2,3,4]

Output: [2,1,4,3]

Explanation:



Example 2:

Input: head = []

Output: []

Example 3:

Input: head = [1]

Output: [1]

Example 4:

Input: head = [1,2,3]

Output: [2,1,3]
 


 


My solution：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def swapPairs(self, head):
        """
        :type head: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        if not head or not head.next:
            return head
        # use a dummy head to return the ultimate head
        dummyhead = ListNode(next=head)
        # use 2 temporary variables
        pre, curr= dummyhead, head
        while curr and curr.next:
            # use temp variable nextt in loop 
            nextt = curr.next

            # exchange
            pre.next = curr.next
            curr.next = curr.next.next
            nextt.next = curr
            
            # next step
            pre = curr
            curr = curr.next

        return dummyhead.next
        
```