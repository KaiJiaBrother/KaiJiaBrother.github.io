---
title: big data notes
tags: Big Data
categories: Notes
abbrlink: b96255d4
date: 2020-03-09 10:05:18
---
# CPU vs GPU vs FPGA
A CPU (central processing unit) works together with a GPU (graphics processing unit) to increase the throughput of data and the number of concurrent calculations within an application.

A CPU can never be fully replaced by a GPU: a GPU complements CPU architecture by allowing repetitive calculations within an application to be run in parallel while the main program continues to run on the CPU. The CPU can be thought of as the taskmaster of the entire system, coordinating a wide range of general-purpose computing tasks, with the GPU performing a narrower range of more specialized tasks (usually mathematical). Using the power of parallelism, a GPU can complete more work in the same amount of time as compared to a CPU.

`The main difference` between CPU and GPU architecture is that a CPU is designed to handle a wide-range of tasks quickly (as measured by CPU clock speed), but are limited in the concurrency of tasks that can be running. A GPU is designed to quickly render high-resolution images and video concurrently.

Because GPUs can perform parallel operations on multiple sets of data, they are also commonly used for non-graphical tasks such as machine learning and scientific computation. Designed with thousands of processor cores running simultaneously, GPUs enable massive parallelism where each core is focused on making efficient calculations.

![cpu vs gpu](/images/cpu_vs_gpu.png)

GPU needs to use cuda, so programming on GPU is more complicated

GPU has better energy efficiency in design than CPU.

Field Programmable Gate Array (FPGA), a reconfigurable integrated circuit.

You can configure the FPGA to become any circuit you want to (as long as it fits on the FPGA). This is quite a bit different than the instruction-based hardware most programmers are used to, such as CPUs and GPUs. Instruction-based hardware is configured via software, whereas FPGAs are instead configured by specifying a hardware circuit.

Low latency
This is where FPGAs are much better than CPUs (or GPUs, which have to communicate via the CPU). With an FPGA it is feasible to get a latency around or below 1 microsecond, whereas with a CPU a latency smaller than 50 microseconds is already very good.


Reference:
1. lectures from university of leeds
2. [omnisci](https://www.omnisci.com/technical-glossary/cpu-vs-gpu)
3. [esciencecenter](https://blog.esciencecenter.nl/why-use-an-fpga-instead-of-a-cpu-or-gpu-b234cd4f309c)
