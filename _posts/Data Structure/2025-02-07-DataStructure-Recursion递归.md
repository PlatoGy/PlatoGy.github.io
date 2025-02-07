---
layout: post
title: Recursion 递归
author: Patrick Gao
date: 2025-2-7 19:20
categories:
  - Data Struture
  - LeetCode Exercise
tags:
  - Binary Tree
  - Recursion
mermaid: true
math: true
pin: false
---
 
参考内容：[代码随想录](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)



### 1.递归算法的三个要素。
每次写递归，都按照这三要素来写，可以保证大家写出正确的递归算法！

1. 确定递归函数的参数和返回值： 确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型。

2. 确定终止条件： 写完了递归算法, 运行的时候，经常会遇到栈溢出的错误，就是没写终止条件或者终止条件写的不对，操作系统也是用一个栈的结构来保存每一层递归的信息，如果递归没有终止，操作系统的内存栈必然就会溢出。

3. 确定单层递归的逻辑： 确定每一层递归需要处理的信息。在这里也就会重复调用自己来实现递归的过程。


### 2.以二叉树的前序遍历为例 Example
```python
class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[int]
        """
        res = []
        # 1. 确定递归函数的参数和返回值: 参数是每次输入的根结点，这里不需要返回值，因为递归中没有用到上一次的返回做参数
        def dfs(parent):
            # 2. 确定终止条件: 若parent为None，则终止
            if not parent:
                return
            # 3. 确定单层递归的逻辑: 每层递归推入本节点的值，并对本节点的左右子节点进行递归遍历操作
            res.append(parent.val)
            dfs(parent.left)
            dfs(parent.right)

        # 根结点是递归起点
        dfs(root)
        return res
        
```