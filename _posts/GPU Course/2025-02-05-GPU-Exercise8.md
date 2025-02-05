---
layout: post
title: GPU Exercise8
author: Patrick Gao
date: 2025-02-05 12:21
categories:
  - MISCADA
  - GPU Course
tags:
  - Term 2 Assignment
mermaid: true
math: true
pin: false
---

## Compiler feedback and the BLIS DGEMM
We’re going to look at how to interact with the compiler to obtain the so that it vectorise a loop the way we want it to.

As our starting point we will use a C version of the GEMM micro-kernel used in the [BLIS framework](https://github.com/flame/blis/).

We will only look at the optimization report (and at the assembly code) produced by the compiler, but we will not run the produced binary. For ease of configuration, we will then use the [Compiler explorer](https://gcc.godbolt.org/), which is an online frontend to multiple versions of all major compilers.

You will find a session of Compiler Explorer targeting the BLIS GEMM micro-kernel if you follow [this link](https://gcc.godbolt.org/z/Y4rYq4jnz). The view is split in three panes:

- on the left, you have a minimal editor with syntax highlighting that contains the C code, which you can modify;
- in the middle, you have a dropdown menu to select the compiler you want to use, a text box to pass compilation options to your chosen compiler, and a view with the generated assembly code; 
- and on the right, you have the output of the compiler.

The compiler is invoked (and the two rightmost views are update) every time changes are made to either the code or the compilation flags. Currently, the code is being compiler with the latest version of the Intel compiler, and the only compilation options are requesting the compiler to show us the optimization report.

## Does vectorisation occur?
Currently, the optimisation report should only contain

`Compiler returned: 0`
which means that no optimisation (and in particular, no vectorisation, has taken place). You can confirm this by looking at the produced assembly code and checking that no vector operations are being used.

## Exercise
 We can try to add some optimization flags to convince the compiler to vectorise. In order to use some large vector register, we can use the -march=common-avx512 flag, which will give us access to vector register that are 512 bit wide and can hold up to eight values of type double. As the default optimisation level is -O0, this will not be enough to convince the compiler to vectorise, but you can try to increase the level to allow vectorisation to kick in. 

## Question
 What does the vectorisation report say? Which loop was vectorised? 

## Vectorising the correct loops
Since the i loop is stride-1, it really makes sense to vectorise the innermost loop. Try and convince the compiler to do so.

## Exercise
 The default blocking factors (MR and NR) are both 1. Given that AVX512 registers can hold eight matrix elements, it makes sense to use larger blocks. Try with some larger blocks. 

## Question
 Which loop, if any, was vectorised this time? 

The optimization report should contain an estimated (potential) speedup at the line that starts with:

`estimated potential speedup:`
## Question
Compare the estimated speedup the compiler reports for the original loop vectorisation choice and the new one.

What do you observe? Is this value in line with your expectations?

## Providing more detailed information
Part of the problem is that the compiler assumes that the array accesses are not aligned to cache line boundaries (or vector registers). The compiler’s cost model is aware that memory accesses are more expensive if the data are not aligned, but this drives some bad decisions. We can help the compiler by letting it know the byte alignment of the arrays.

## Exercise
We can do this by using the built-in function __builtin_assume_aligned (you can find the manual for the corresponding GCC built-in function here) to tell the compiler that the given pointer is 64-byte aligned.

For example, to allow the compiler to assume that A is 64-bit aligned you can use

```__builtin_assume_aligned(A, 64);```
or

```double *A_aligned = (double *)__builtin_assume_aligned(A, 64);```
to avoid the compilation warning.

## Question
Try adding alignment assumptions before the start of the loop nest.

What happens to the estimated speedup?

## Putting it together
The subdirectory code blis-gemm/ (which you can download as a .tar.bz2 archive) contains a complete implementation of this scheme, which you can run on Hamilton. You can edit the parameters.h file to set the blocking parameters MR and NR, and you can also modify the source file micro-kernel.c to make the changes you found beneficial using Compiler Explorer.

## Exercise
To start with, all five blocking parameters in parameters.h are set to

Compile the code. Run for a range of matrix sizes between 100 and 2000 (check the bench target in the Makefile to streamline this). What performance do you observe?
## Exercise
 Now try changing setting MC to 128, KC to 256, and NC to 1024, and using your good parameters for MR and NR. Recompile and rerun the benchmarking. What performance do you observe now? 

## Exercise
In addition to having good parameters, try aligning the memory of the pointers or adding any pragmas you found helpful in the Compiler Explorer part of the exercise to the micro kernel in micro-kernel.c. Rerun the same experiments again. What performance do you observe now?

You might needed to stop the micro_kernel from being inlined by the Intel compiler for really good performance. In order to do that, you need to change the signature to

```c
__attribute__((noinline))
static void micro_kernel(...)
```
Rerun again, do you observe any further differences?

How close to peak performance does the code get?