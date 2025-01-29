---
layout: post
title: 707-design-linked-list
author: Patrick Gao
date: 2025-01-29 20:44
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Linked List
mermaid: true
math: true
pin: false
---
Design your implementation of the linked list. You can choose to use a singly or doubly linked list.
A node in a singly linked list should have two attributes: val and next. val is the value of the current node, and next is a pointer/reference to the next node.
If you want to use the doubly linked list, you will need one more attribute prev to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.

Implement the MyLinkedList class:

MyLinkedList() Initializes the MyLinkedList object.
int get(int index) Get the value of the indexth node in the linked list. If the index is invalid, return -1.
void addAtHead(int val) Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
void addAtTail(int val) Append a node of value val as the last element of the linked list.
void addAtIndex(int index, int val) Add a node of value val before the indexth node in the linked list. If index equals the length of the linked list, the node will be appended to the end of the linked list. If index is greater than the length, the node will not be inserted.
void deleteAtIndex(int index) Delete the indexth node in the linked list, if the index is valid.
 

Example 1:

Input
["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"]
[[], [1], [3], [1, 2], [1], [1], [1]]
Output
[null, null, null, null, 2, null, 3]

Explanation
MyLinkedList myLinkedList = new MyLinkedList();
myLinkedList.addAtHead(1);
myLinkedList.addAtTail(3);
myLinkedList.addAtIndex(1, 2);    // linked list becomes 1->2->3
myLinkedList.get(1);              // return 2
myLinkedList.deleteAtIndex(1);    // now the linked list is 1->3
myLinkedList.get(1);              // return 3
 


My solution：

```python
class MyLinkedList(object):

    def __init__(self):
        self.head = None
        self.dummyhead = ListNode(next=self.head)
    def get(self, index):
        """
        :type index: int
        :rtype: int
        """
        i = 0
        tmp = self.dummyhead
        while tmp.next:
            if i == index:
                break
            tmp = tmp.next
            i += 1
        if i == index and tmp.next:
            return tmp.next.val
        else:
            return -1

    def addAtHead(self, val):
        """
        :type val: int
        :rtype: None
        """
        node = ListNode(val=val)
        node.next = self.dummyhead.next
        self.dummyhead.next = node
        

    def addAtTail(self, val):
        """
        :type val: int
        :rtype: None
        """
        tmp = self.dummyhead
        node = ListNode(val = val)
        while tmp.next != None:
            tmp = tmp.next
        tmp.next = node

    def addAtIndex(self, index, val):
        """
        :type index: int
        :type val: int
        :rtype: None
        """
        i = 0
        node = ListNode(val=val)
        tmp = self.dummyhead
        while tmp.next:
            if i == index:
                break
            tmp = tmp.next
            i += 1

        if i == index:
            node.next = tmp.next
            tmp.next = node

    def deleteAtIndex(self, index):
        """
        :type index: int
        :rtype: None
        """
        i = 0
        tmp = self.dummyhead
        while tmp.next:
            if i == index:
                break
            tmp = tmp.next
            i += 1
        
        if i == index and tmp.next:
            tmp.next = tmp.next.next

# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```

However, if the indexs of deleteAtIndex() and get() are bigger than the size of the linked list, we will waste a lot of time on counting the size of the linked list. Therefore, using a property named `size` is useful, and we can modify it when we change the linked list.

## Optimize:
```python
class MyLinkedList(object):

    def __init__(self):
        self.dummyhead = ListNode(next=None)
        self.size = 0
    def get(self, index):
        """
        :type index: int
        :rtype: int
        """
        if index > self.size:
            return -1
        i = 0
        tmp = self.dummyhead
        while tmp.next:
            if i == index:
                break
            tmp = tmp.next
            i += 1
        if i == index and tmp.next:
            return tmp.next.val
        else:
            return -1

    def addAtHead(self, val):
        """
        :type val: int
        :rtype: None
        """
        node = ListNode(val=val)
        node.next = self.dummyhead.next
        self.dummyhead.next = node
        self.size += 1

    def addAtTail(self, val):
        """
        :type val: int
        :rtype: None
        """
        tmp = self.dummyhead
        node = ListNode(val = val)
        while tmp.next != None:
            tmp = tmp.next
        tmp.next = node
        self.size += 1

    def addAtIndex(self, index, val):
        """
        :type index: int
        :type val: int
        :rtype: None
        """
        i = 0
        node = ListNode(val=val)
        tmp = self.dummyhead
        while tmp.next:
            if i == index:
                break
            tmp = tmp.next
            i += 1

        if i == index:
            node.next = tmp.next
            tmp.next = node
            self.size += 1

    def deleteAtIndex(self, index):
        """
        :type index: int
        :rtype: None
        """
        if index > self.size:
            return
        i = 0
        tmp = self.dummyhead
        while tmp.next:
            if i == index:
                break
            tmp = tmp.next
            i += 1
        
        if i == index and tmp.next:
            tmp.next = tmp.next.next
            self.size -= 1

# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```