---
layout: post
title: Python Deque
author: Patrick Gao
date: 2025-2-4 09:20
categories:
  - Data Struture
tags:
  - Python
mermaid: true
math: true
pin: false
---

## 1.Introduction

collections.deque（双端队列）是 Python 提供的一个 高效 的 双端队列，相比 list 在 头部操作（插入/删除） 速度更快，适用于 队列（queue） 和 栈（stack） 场景。

## 2.Use 
### 2.1 导入
`from collections import deque`

### 2.2 创建deque
```python
# 创建一个空的 deque
dq = deque()

# 直接用列表初始化 deque
dq = deque([1, 2, 3])
print(dq)  # 输出: deque([1, 2, 3])

```

### 2.3 添加元素
```python
dq = deque([1, 2, 3])
dq.append(4)       # 在队尾添加
dq.appendleft(0)   # 在队首添加
print(dq)  # 输出: deque([0, 1, 2, 3, 4])

```

### 2.4 删除元素
 ```python
dq = deque([1, 2, 3, 4])
print(dq.pop())     # 输出: 4（删除队尾元素）
print(dq.popleft()) # 输出: 1（删除队首元素）
print(dq)           # 输出: deque([2, 3])

```       

### 2.5 添加多个元素
```python
dq = deque([2, 3])
dq.extend([4, 5, 6])       # 添加到队尾
dq.extendleft([1, 0])      # 逆序添加到队首
print(dq)  # 输出: deque([0, 1, 2, 3, 4, 5, 6])


```

### 2.6 旋转移动
```python
dq = deque([1, 2, 3, 4, 5])
dq.rotate(2)   # 右移2步
print(dq)      # 输出: deque([4, 5, 1, 2, 3])

dq.rotate(-1)  # 左移1步
print(dq)      # 输出: deque([5, 1, 2, 3, 4])

```

## 3.Deque 与 List 对比

操作	deque	list
队尾插入	O(1)	O(1)
队尾删除	O(1)	O(1)
队首插入	O(1)	O(n)
队首删除	O(1)	O(n)
索引访问	O(n)	O(1)
