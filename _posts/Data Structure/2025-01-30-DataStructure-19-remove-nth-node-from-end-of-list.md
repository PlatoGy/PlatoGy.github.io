---
layout: post
title: 19-remove-nth-node-from-end-of-list
author: Patrick Gao
date: 2025-01-30 13:30
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Linked List
mermaid: true
math: true
pin: false
---
Given the head of a linked list, remove the nth node from the end of the list and return its head.

 

Example 1:


Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Example 2:

Input: head = [1], n = 1
Output: []
Example 3:

Input: head = [1,2], n = 1
Output: [1]
 

Constraints:

The number of nodes in the list is sz.
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz

 


 


My solution：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: Optional[ListNode]
        :type n: int
        :rtype: Optional[ListNode]
        """
        if not head:
            return head
        dummyhead = ListNode(next = head)
        slowIndex = dummyhead
        fastIndex = head
        size = 0
        # calculate the size of the linked list
        while fastIndex:
            size += 1
            fastIndex = fastIndex.next
        i = 0
        while slowIndex.next:
            # delete the (size - n)th node 
            if i == size - n:
                slowIndex.next = slowIndex.next.next
                break
            else:
                i += 1
                slowIndex = slowIndex.next
        return dummyhead.next
        
```

Optimization:
Use only 1 loop to implement：
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: Optional[ListNode]
        :type n: int
        :rtype: Optional[ListNode]
        """
        if not head:
            return head
        dummyhead = ListNode(next = head)
        slowIndex = dummyhead
        fastIndex = head
        i = 0
        while fastIndex:
            # the distance between fast and slow index is n
            if i == n:
                slowIndex = slowIndex.next
            else:
                i += 1
            fastIndex = fastIndex.next
            
        slowIndex.next = slowIndex.next.next
        return dummyhead.next

```