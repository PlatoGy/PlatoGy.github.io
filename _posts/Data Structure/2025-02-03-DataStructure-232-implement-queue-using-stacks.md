---
layout: post
title: 232-implement-queue-using-stacks
author: Patrick Gao
date: 2025-2-3 19:20
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Quene and Stack
mermaid: true
math: true
pin: false
---

 Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise.
Notes:

You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.
 

Example 1:

Input
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 1, 1, false]

Explanation
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false





### My solution：
class MyQueue(object):

    def __init__(self):
        self.mainList = []
        self.supList = []
        self.length = 0

    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        self.mainList.append(x)
        self.length += 1


    def pop(self):
        """
        :rtype: int
        """
        tmp = self.length
        while tmp > 1:
            self.supList.append(self.mainList.pop())
            tmp -= 1
        res = self.mainList.pop()
        self.length -= 1
        tmp -= 1
        while tmp != self.length:
            self.mainList.append(self.supList.pop())
            tmp += 1
        
        return res
    def peek(self):
        """
        :rtype: int
        """
        tmp = self.length
        while tmp > 1:
            self.supList.append(self.mainList.pop())
            tmp -= 1
        res = self.mainList.pop()
        self.mainList.append(res)
        while tmp != self.length:
            self.mainList.append(self.supList.pop())
            tmp += 1
        return res

    def empty(self):
        """
        :rtype: bool
        """
        return True if self.length == 0 else False


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
        

