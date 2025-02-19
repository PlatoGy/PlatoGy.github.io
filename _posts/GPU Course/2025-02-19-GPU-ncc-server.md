---
layout: post
title: 在 NCC 使用 GPU 计算的注意事项
author: Patrick Gao
date: 2025-02-19 12:17
categories:
  - MISCADA
  - GPU Course
tags:
  - GPU Programming
mermaid: true
math: true
pin: false
---

## 1. 连接到 NCC

在使用 NCC 之前，你需要通过命令行连接到 NCC。建议先查看 Learn Ultra 页面，获取具体的连接方式。通常，你需要通过 SSH 连接：

```bash
ssh your_username@ncc1.clients.durham.ac.uk
```

如果 SSH 连接有问题，检查是否需要使用 ProxyCommand 或 ProxyJump（可能需要先连接 hamilton）。

## 2. 申请 GPU 计算资源

在 NCC 登录节点上，你不能直接运行 GPU 代码，需要使用 Slurm 申请计算资源：
```bash
srun -c 1 --gres=gpu:pascal:1 --partition=tpg-gpu-small --pty /bin/bash
```
参数解析

```
-c 1：申请 1 个 CPU 核心。
--gres=gpu:pascal:1：申请 1 张 Pascal 系列 GPU。
--partition=tpg-gpu-small：使用 tpg-gpu-small 分区（相对较空闲）。
--pty /bin/bash：启动交互式 bash 终端。
```

等待时间
NCC 的 GPU 资源紧张，尤其是 Turing 和 Ampere 服务器，选择 gpu:pascal 通常更快。
如果 srun 长时间没有响应，可能是 作业队列堵塞，你需要等待或者使用 squeue 查看当前的任务情况：
```bash
squeue -u your_username
```

## 3. NCC 与 Hamilton 的主要区别

NCC 登录节点不允许直接运行计算任务：
不能运行 GPU 代码（会失败）。
不能在登录节点测试 CPU 代码，否则可能会受到处罚。
必须使用 Slurm 提交作业或申请交互式会话。
Hamilton 的登录节点和计算节点硬件相同：
在 Hamilton，你可以直接在登录节点编译和测试代码。
在 NCC，必须进入计算节点，否则无法访问 GPU。
NCC 需要指定 QoS 参数：
推荐使用 debug QoS 来调试代码：
```bash
sbatch --qos=debug my_job_script.sh
```
## 4. 在 NCC 编译 CUDA 代码

NCC 提供多个 软件模块（modules） 来支持 CUDA、OpenMP 和 SYCL 编程。

加载 CUDA 编译环境
```bash
module load cuda/12.0
nvcc your_source_code.cu -o your_executable
module load cuda/12.0：加载 CUDA 12.0 版本（根据需求可能需要不同版本）。
nvcc your_source_code.cu -o your_executable：用 nvcc 编译 CUDA 代码。
```
## 5. 编译 OpenMP 代码（支持 GPU 计算）
```bash

module load nvidia-hpc
nvc++ -fopenmp -mp=gpu test.cpp -o test_executable
module load nvidia-hpc：加载 NVIDIA HPC 编译器。
-fopenmp：启用 OpenMP 并行计算。
-mp=gpu：让 OpenMP 代码运行在 GPU 上。
```
调整 OpenMP 线程
你可以通过以下环境变量调整 OpenMP 线程数：
```bash
export OMP_NUM_THREADS=8
export OMP_NUM_TEAMS=2
export OMP_THREAD_LIMIT=16
```
注意：

这些值是 上限，Slurm 可能会根据作业资源修改它们。
具体使用多少线程，取决于计算资源

## 6. 在 NCC 编译 SYCL 代码

```bash
module load llvm-clang
module load cuda/11.5
clang++ -fsycl -fsycl-targets=nvptx64-cuda my_source_code.cpp -o my_executable
module load llvm-clang：加载 LLVM Clang 编译器（支持 SYCL）。
module load cuda/11.5：加载 CUDA 11.5 以支持 SYCL 运行时。
-fsycl -fsycl-targets=nvptx64-cuda：指定 SYCL 目标平台（NVIDIA CUDA）。
```
## 7. 任务管理与作业提交

如果 不想使用交互式会话（srun），你可以用 sbatch 提交批处理作业。

示例 Slurm 批处理脚本
```bash
#!/bin/bash
#SBATCH --job-name=my_gpu_job
#SBATCH --partition=tpg-gpu-small
#SBATCH --gres=gpu:pascal:1
#SBATCH --cpus-per-task=4
#SBATCH --mem=16G
#SBATCH --time=01:00:00
#SBATCH --output=job_output.txt

module load cuda/12.0
nvcc my_cuda_program.cu -o my_cuda_executable
./my_cuda_executable
然后提交作业：
```

```bash
sbatch my_job_script.sh
```

# 查看作业状态：

```bash
squeue -u your_username
```

# 取消作业：

```bash
scancel job_id
```