---
layout: post
title: GPU Exercise4
author: Patrick Gao
date: 2025-01-22 19:35
categories:
  - MISCADA
tags:
  - GPU Course
  - Term 2 Assignment
mermaid: true
math: true
pin: false
---

# Roofline Analysis of Matrix–Vector Multiplication

The goal of this exercise is to perform a **roofline analysis** of matrix–vector multiplication. We will explore:  
1. The effect of compiler flags on the performance of the generated code.  
2. Whether the performance depends on the problem size.  
3. The impact of loop blocking.

---

## Background

The file `dmvm.c` contains a C implementation of matrix–vector multiplication, which computes:

**y = A × x**

for an \( n_{\text{row}} \times n_{\text{col}} \) rectangular matrix of doubles. The code accepts two command-line arguments:  

- The number of rows.
- The number of columns.  

When executed, the program generates matrices, performs the computation, and prints performance information. For example, compiling and running with `./dmvm 1000 2000` might produce output like:  
```plaintext
1019 1000 2000 6491.23
```

## Output Columns Explained

The program produces output with the following four columns:  

1. **Number of iterations**: The number of iterations the test was run for.  
2. **Number of rows**: The number of rows in the matrix.  
3. **Number of columns**: The number of columns in the matrix.  
4. **Performance**: The performance in MFLOPS/s.

---

## Downloading and Compiling the Code

We will use the **GCC compiler** for this exercise. In addition to the `likwid` module, make sure to load the module with the compiler.

## Compilation Without Any Optimizations

First, compile the code without any optimizations.  

You can now run the `dmvm` binary as follows:
```bash
./dmvm 4000 4000
```

## Obtain the Machine and Code Characteristics

To perform a roofline analysis, both machine and code characteristics need to be determined.

## Exercises:

1. **Measure Memory Bandwidth**  
   Use the **triad benchmark** from `likwid-bench` to measure the main memory streaming bandwidth.

2. **Compute Peak Floating-Point Throughput**  
   - The maximum frequency of a single core on a Hamilton compute node is **3.35GHz**.  
   - Under ideal conditions, each core can issue **two double-precision FMAs** (fused multiply-add instructions) per cycle.

3. **Determine Best-Case Arithmetic Intensity**  
   Read the `dmvm` function in the code and calculate the best-case arithmetic intensity by:  
   - Counting **data accesses** using the perfect cache model.  
   - Counting **floating-point operations** performed.

---

## Produce a Roofline Plot of `-O0` Compiled Code

## Exercise:

1. Fix the number of columns: \( n_{\text{col}} = 10000 \).  
2. Measure the performance of your `dmvm` binary over a range of row sizes from **1000 to 100,000**.  
3. Plot the resulting data on a **roofline plot**.

## Question:  
What do you think your next step in optimizing the code should be?

---

## Better Compiler Options

## Steps:

1. Increase the compiler optimization level (e.g., `-O1`, `-O2`, `-O3`).  
2. Explore other optimization options provided by the compiler.  
3. Identify and note the options that produced the **fastest results**.

## Exercise:

1. Add the results of these runs to your roofline plots.  
2. Analyze and answer the following:

   - **Question**:  
     - Is the performance for any of these options independent of the problem size?  
     - What do you think the bottleneck for this algorithm is?

---

## Loop Blocking for Out-of-Cache Performance

## Observations:

When the number of rows becomes too large:  
1. The performance of the code drops by almost **a factor of two**.  
2. Some vector data (accessed more than once) no longer fits in cache.

## Exercise:

1. Use the **pessimal cache model** to calculate the **worst-case arithmetic intensity**.  
2. Add these new data points to your roofline plot.

## Loop Blocking/Tiling:

To address the issue, traverse the data in a cache-aware order.  
For loop-based code, this is known as **loop blocking** or **tiling**.  

1. Examine the `dmvm-blocked.c` implementation.  
2. Compile it with the **best compiler options** identified earlier:  
```bash
   gcc -o dmvm-blocked dmvm-blocked.c <best-options>
   
```

## Exercise: Worst-Case Arithmetic Intensity

1. Use the **pessimal cache model** to compute the **worst-case arithmetic intensity**.  
2. Add these new data points to your **roofline plot**.

---

## Loop Blocking/Tiling for Cache Awareness

To address performance issues caused by large row sizes, traverse the data in a **cache-aware order**.  
For loop-based code, this approach is called **loop blocking** or **tiling**.

### Steps:

1. Examine the `dmvm-blocked.c` implementation.  
2. Compile the code using the **best compiler options** identified earlier:  
   ```bash
   gcc -o dmvm-blocked dmvm-blocked.c <best-options>

## Exercise: Roofline Plot for `dmvm-blocked`

1. Fix the number of columns: \( n_{\text{col}} = 10000 \).  
2. Measure the performance of the `dmvm-blocked` binary over a range of row sizes from **1000 to 100,000**.  
3. Plot the resulting data on a **roofline plot**.  

   - **Observation:** The performance should now be largely **insensitive to the number of rows**.

## Questions: