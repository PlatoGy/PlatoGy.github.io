---
layout: post
title: 性能优化PPT3-roofline模型
author: Patrick Gao
date: 2025-03-28 18:57
categories:
  - MISCADA
  - GPU Course
tags:
  - GPU Programming
mermaid: true
math: true
pin: false
---

# Lecture 3: Roofline Models

**Lecturer**: Anne Reinarz

---

## 🚀 Exercise 2: Results & Interpretation

- **Vectorised addition**
  - 每个周期加载 1 个 32Byte（8个float）
  - 累加器存在寄存器中
  - 需持续带宽约 107GB/s

- **带宽 vs. 浮点性能限制**
  - **L1 Cache (<32kB)**: 370 GB/s ≈ 22 float/Flop ⇒ *浮点运算为瓶颈*
  - **L2 Cache (<512kB)**: 100 GB/s ≈ 6.25 float/Flop ⇒ *峰值约 27 GFlop/s*
  - **L3 Cache (<16MB)**: 78 GB/s ≈ 4.45 float/Flop ⇒ *峰值约 19 GFlop/s*
  - **Main Memory**: 17.5 GB/s ≈ 1 float/Flop ⇒ *峰值约 4.5 GFlop/s*

---

## 📈 AVX Throughput with Bandwidth-Induced Limits

- 测量 AVX 吞吐量的不同缓存级别限制（L1/L2/L3/RAM）

---

## 🧠 Memory/Node Topology

- 使用 `likwid-topology` 获取拓扑结构

---

## 🧪 Exercise 3: Cache vs Cores

- 测量 L1/L2/L3/RAM 带宽在不同核心数量下的表现（1 vs 8 memory domains）

---

## 🧩 硬件架构总结

### 性能考量因素
- 指令数量
- 执行效率
- 数据传输对运行时间的影响

### 硬件拓扑复杂性
- 多层并行：
  - Sockets: 1-4 CPUs
  - Cores: 4-32 核
  - Vectorization: 每个向量寄存器含 2-16 float
  - Superscalar: 每周期 2-8 条指令

---

## ⚙️ 资源类型

| 类型 | 特性 | 例子 |
|------|------|------|
| Scalable (线性扩展) | 私有资源 | FPU, CPU 核 |
| Saturating (饱和扩展) | 共享资源 | L3, RAM |

- **瓶颈常由饱和资源决定**

---

## 🧪 clcopy vs. STREAM 基准测试

- `clcopy`:
  - 每缓存行只访问一个字节 ⇒ 不现实

- 推荐使用：`STREAM TRIAD`
  ```c
  a[i] = b[i] * alpha + c[i];  // 2 Flops, 2 loads, 1 store
  ```

---

## 🔁 简化的 Loop 模型

- 循环代码简化为：
  - M Flops + B Bytes 数据传输
  - **运算强度** \( I_c = \frac{M}{B} \)

---

## 🌄 Roofline 模型

- 描述性能瓶颈：
  ```text
  P = min(P_peak, I_c × b_s)
  ```

- 来源：Williams et al. (CACM, 2009)

---

## 🧰 应用 Roofline 的三步骤

1. 测量 P_peak, b_s, I_c
2. 绘制 Roofline 图
3. 选择优化策略（是否矢量化、提升 I_c 等）

---

## 📏 如何估算 Roofline 三要素

### 1. Streaming Bandwidth (b_s)
- 通常通过 `STREAM` 测量
- 或用内存通道数 × 频率 × 8

### 2. 浮点性能 (P_peak)
- 需知架构细节（如 AMD Zen2）
- 示例：
  - SIMD FMA（双发）：
    ```
    3.35 GHz × 2 × 4 × 2 = 53.6 GFlop/s
    ```
  - 仅DIV（单发）：
    ```
    3.35 GHz × 1 × 4 = 13.4 GFlop/s
    ```

---

## 📐 计算运算强度 I_c

### 方法一：性能计数器

### 方法二：纸面分析
- 统计 Flop 数 (M)
- 统计数据访问字节数 (B)
- 计算：
  ```text
  I_c = M / B
  ```

---

## 🔍 示例分析

```c
for (int i = 0; i < N; i++) {
  for (int j = 0; j < M; j++) {
    a[j] = b[i]*c[i] + d[i]*a[j];
  }
}
```

- 每次迭代：3 Flops, 3 reads, 1 write
- **内存访问模型**：
  - *理想 Cache*: 8×(2M + 3N) 字节
  - *最坏 Cache*: 8×(2MN + 3MN) 字节



## 如何计算性能P（单位：Flops/s ）？


## 一、Streaming Bandwidth（\( b_s \)）

即：**内存子系统的实际可用带宽**（单位：Bytes/s）

### ✅ 方法 1：使用 STREAM Benchmark（推荐）

- 可通过 [`likwid-bench`] 工具使用：
  ```bash
  likwid-bench -t stream -w S0:1 -C 0
  ```

- 示例输出：
  ```
  Function    Rate (MB/s)
  Triad:      25000
  ```
  ⇒ 转换单位：
  ```text
  b_s = 25 × 10^9 Bytes/s = 25 GB/s
  ```

---

### ✅ 方法 2：估算法（理论计算）

公式：
\[
b_s = \text{Memory Frequency} × \text{Channels} × 8
\]

例如 DDR4-3200 双通道：
\[
3.2 × 10^9 × 2 × 8 = 51.2 GB/s
\]

⚠️ 实际带宽只有理论的 60~80%，建议使用实测值！

---

## 二、峰值浮点性能（\( P_{\text{peak}} \)）

即：**CPU 理论最大浮点运算能力**（单位：Flops/s）

### ✅ 公式（以 SIMD FMA 为例）：

\[
P_{\text{peak}} = \text{Clock Frequency} × \text{Issue Rate} × \text{Vector Width (Flops)}
\]

#### 示例：AMD Zen 2 架构

- 频率 = 3.35 GHz
- 每周期双发 FMA（2条指令）
- 每条 SIMD FMA：4 doubles × 2 Flops = 8 Flops

\[
P_{\text{peak}} = 3.35 × 10^9 × 2 × 8 = 53.6 GFlops/s
\]

---

### 多核系统（总峰值）

\[
P_{\text{peak, total}} = P_{\text{peak, per\ core}} × \text{核心数量}
\]

---

## 三、最终性能 P 的计算

Roofline 模型公式：
\[
P = \min(P_{\text{peak}}, I_c × b_s)
\]

- \( I_c \)：运算强度（Flops / Byte）
- \( b_s \)：带宽（Bytes / s）
- \( P_{\text{peak}} \)：峰值浮点性能

---