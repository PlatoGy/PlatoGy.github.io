---
layout: post
title: GPU Exercise5
author: Patrick Gao
date: 2025-01-22 19:35
categories:
  - MISCADA
  - GPU Course
tags:
  - Term 2 Assignment
mermaid: true
math: true
pin: false
---

## Verifying a model with measurements
The goal of this exercise is to verify our model for the number of loads and stores in a stream benchmark using performance counters, accessed via likwid-perfctr.

## Background
In stream.c, you can find a C implementation of the STREAM TRIAD benchmark. The code provides a scalar, an SSE, and AVX implementations of the loop
```c
double *a, *b, *c;
...
for (i = 0; i &lt; N; i++) {
  c[i] = c[i] + a[i] * b[i];
}
```
Once compiled, the program can be called as ./stream <N> <LOOP_TYPE>, where <N> is the number of elements in the three arrays and <LOOP_TYPE> is one of sca, sse, avx, fma, align, or unalign. See ./stream -h (or the source code itself) for more details on this option.

We will measure the number of loads and stores for this loop using likwid-perfctr. In order to do so, we need to compile the code appropriately.

## Compiling with likwid annotations enabled
The code is annotated with likwid-specific markers around the relevant loops. This is to ensure that counters are measured only for the portions of codes we are interested in profilin We therefore need to enable these when compiling. As before we load the likwid module with module load likwid/5.2.0.

We can safely compile this code with GCC, load the GCC module with module load gcc/12.2 and run:

`gcc -std=c99 -mfma -O1 -DLIKWID_PERFMON -fno-inline -march=native -o stream stream.c -llikwid`
The flag -DLIKWID_PERFMON adds a new symbol in the preprocessor which will turn on the likwid markers. We then also need to link against the likwid runtime library with -llikwid. To ensure that this library is available when you run the code, you should load the likwid module on the compute node (or run module load likwid/5.2.0 in your batch submission script).

For this exercise, likwid-perfctr does not give us an appropriate predefined group. Instead, we must use a low-level counter directly. The relevant counters are LS_DISPATCH_LOADS for loads and LS_DISPATCH_STORES for stores. We must specify a group string, of the form <counter>:<register>, where <counter> is the performance counter we want to use (for example LS_DISPATCH_LOADS) and <register> is the register in which we want to save it. For memory operations we can use the registers PMC0 and PMC1 (possibly others, but these will suffice).

A complete command line to measure the number of loads is

`likwid-perfctr -m -g "LS_DISPATCH_LOADS:PMC0" -C 0 ./stream 1000000 sca`
This tell liwid-perfctr to enable the marker API (with -m), to count the LS_DISPATCH_LOADS event in PMC0, and to pin the executable to core zero (with -C 0). This final part is necessary so that the operating system does not move the executable from one core to another during execution, which would break our measurements. The command should produce an output like the following:
```
--------------------------------------------------------------------------------
CPU name:       AMD EPYC 7702 64-Core Processor
CPU type:       AMD K17 (Zen2) architecture
CPU clock:      2.00 GHz
--------------------------------------------------------------------------------
WARN: Skipping region SSE-0 for evaluation.
WARN: Skipping region AVX-0 for evaluation.
WARN: Skipping region FMA-0 for evaluation.
WARN: Skipping region UNALIGNED-0 for evaluation.
WARN: Skipping region ALIGNED-0 for evaluation.
WARN: Regions are skipped because:
      - The region was only registered
      - The region was started but never stopped
      - The region was never started but stopped
sca loop, sum 3.33328e+17
--------------------------------------------------------------------------------
Region Scalar, Group 1: Custom
+-------------------+------------+
|    Region Info    | HWThread 0 |
+-------------------+------------+
| RDTSC Runtime [s] |   0.001400 |
|     call count    |          1 |
+-------------------+------------+
 
+---------------------+---------+--------------+
|        Event        | Counter |  HWThread 0  |
+---------------------+---------+--------------+
| Runtime (RDTSC) [s] |   TSC   | 1.400006e-03 |
|  LS_DISPATCH_LOADS  |   PMC0  |      3005392 |
+---------------------+---------+--------------+
```
This measurement at least, aligns with what we expected, since we see about 3000000 loads.

## Question
How does the number of loads change if you use the SSE, AVX, or FMA versions of the code?
How many stores do you measure?