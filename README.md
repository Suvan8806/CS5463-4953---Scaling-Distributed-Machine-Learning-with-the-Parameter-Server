# CS 5463/4953 – Survey-Based Term Project
## Topic Selection Write-Up
**Date:** March 6, 2026

---

## Survey Title
Survey on Distributed Machine Learning: Systems, Algorithms, and Scalability

## Category
Distributed Machine Learning — Parallelism Strategies, Communication, and Scalability

---

## Problem Statement

As machine learning models and datasets continue to grow in scale, training on a single machine has become computationally infeasible. Distributed machine learning (DML) addresses this by spreading both data and computation across many machines — but doing so efficiently introduces a set of fundamental challenges: How should model parameters be partitioned and shared? How should workers communicate gradient updates? How do we balance synchronization correctness against system performance? And how do we handle failures at scale? These questions have driven a rich body of research spanning distributed systems, parallel computing, and machine learning theory. This survey examines the landscape of distributed ML — from foundational parallelism concepts and early systems to modern frameworks capable of training models with hundreds of billions of parameters across thousands of GPUs.

---

## Scope of the Survey

This survey covers the **broad landscape of distributed machine learning**, with particular attention to the systems and algorithmic techniques that enable large-scale training. It is grounded in the Parameter Server (PS) framework — specifically the Li et al. OSDI 2014 paper *"Scaling Distributed Machine Learning with the Parameter Server"* — as a central case study, but extends outward to survey the wider field. The survey will cover: (i) foundational parallelism strategies — data parallelism, model parallelism, and pipeline parallelism; (ii) parameter server architectures and their consistency models (BSP, SSP, asynchronous); (iii) AllReduce-based communication as an alternative to the PS paradigm; (iv) gradient compression and communication efficiency techniques; (v) modern large-scale training frameworks including TensorFlow, Horovod, PyTorch Distributed, DeepSpeed, and Megatron-LM; and (vi) open challenges in fault tolerance, scalability, and convergence at scale. The survey aims to synthesize existing literature and map the evolution of distributed ML from early parameter servers to today's trillion-parameter training systems.

---

## Key Topics to be Covered

- Data parallelism, model parallelism, and pipeline parallelism
- Parameter server architecture: server groups, worker nodes, push/pull communication
- Consistency models: BSP, SSP, eventual consistency, and asynchronous SGD
- AllReduce vs. Parameter Server: topology and communication trade-offs
- Gradient compression: sparsification, quantization, and low-rank methods
- Fault tolerance: vector clocks, chain replication, and checkpoint/restart
- Modern frameworks: TensorFlow, Horovod, PyTorch DDP, DeepSpeed/ZeRO, Megatron-LM
- Scaling laws and convergence guarantees under relaxed consistency

---

## Primary Reference Paper
Li, M., Andersen, D. G., Park, J. W., Smola, A. J., et al. (2014). *Scaling Distributed Machine Learning with the Parameter Server.* OSDI 2014.
The paper and presentation slides are included in this repository as foundational reference material.

## GitHub Repository
All papers, slides, and bibliography are available at:
https://github.com/Suvan8806/CS5463-4953---Scaling-Distributed-Machine-Learning-with-the-Parameter-Server