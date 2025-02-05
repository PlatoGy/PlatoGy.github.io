---
layout: post
title: 239-sliding-window-maximum
author: Patrick Gao
date: 2025-2-5 12:20
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Stack and Queue
mermaid: true
math: true
pin: false
---
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

 

Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

Example 2:

Input: nums = [1], k = 1
Output: [1]
 





### My solution：
```python
class Solution(object):
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        maxList = []
        stack = []
        maxNum = float('-inf')
        for i in range(k):
            stack.append(nums[i])
            maxNum = maxNum if nums[i] <= maxNum else nums[i]
        maxList.append(max(stack))

        i = k

        while i < len(nums):
            out_num = stack.pop(0)
            in_num = nums[i]
            stack.append(in_num)
            if out_num == maxList[-1]:
                maxList.append(max(stack))
            else:
                bigger_num = max(in_num,maxList[-1])
                maxList.append(bigger_num)
            i += 1
            
        return maxList
            
```
Sadly it's out of time limit. It must because of the `max` function.      

Time Complexity: O(n*k)
Space Complexity: O(n+k)

### Best solution：
Use a supportive quene which is in a decrease sort.

```python
from collections import deque
class MyQueue():
    def __init__(self):
        self.queue = deque()
    def push(self,value):
        while self.queue and value > self.queue[-1]:
            self.queue.pop()
        self.queue.append(value)
    def pop(self,value):
        if self.queue and value == self.queue[0]:
            self.queue.popleft()

    def front(self):
        return self.queue[0]

class Solution(object):
    
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        que = MyQueue()
        result = []
        for i in range(k): #先将前k的元素放进队列
            que.push(nums[i])
        result.append(que.front()) #result 记录前k的元素的最大值
        for i in range(k, len(nums)):
            que.pop(nums[i - k]) #滑动窗口移除最前面元素
            que.push(nums[i]) #滑动窗口前加入最后面的元素
            result.append(que.front()) #记录对应的最大值
        return result
            

```
Time Complexity: O(n)
Space Complexity: O(k)