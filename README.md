# CS 5463/4953 – Survey-Based Term Project
## Topic Selection Write-Up
**Date:** March 6, 2026

---

## Survey Title
Survey on Parameter Distribution and Synchronization Strategies in Distributed Machine Learning

## Category
Distributed Deep Learning — Parameter Server Architectures and Gradient Synchronization

---

## Problem Statement

Training large-scale machine learning models requires distributing both data and computation across many machines. A central and unsolved tension in this setting is how to keep model parameters, which may number in the billions, synchronized across worker nodes efficiently, without sacrificing training accuracy or system fault tolerance. Two dominant paradigms have emerged to address this: the **Parameter Server (PS)** architecture, where dedicated server nodes hold global parameters that workers push gradients to and pull updates from; and **collective communication** approaches like AllReduce, where workers synchronize directly with each other in a ring or tree topology. Each approach makes fundamentally different trade-offs between communication cost, consistency guarantees, and fault tolerance. This survey examines how these trade-offs have been navigated across the history of distributed ML systems, with a focus on the design of consistency models — from fully synchronous Bulk Synchronous Processing (BSP), to bounded-delay models like Stale Synchronous Parallel (SSP), to fully asynchronous approaches.

---

## Scope of the Survey

This survey focuses specifically on **how model parameters are distributed and kept synchronized** across nodes during distributed training — a narrower and more distinct scope than a general survey of distributed ML systems. It will cover: (i) early key-value based parameter sharing architectures; (ii) the third-generation Parameter Server framework and its consistency, communication, and fault tolerance mechanisms; (iii) competing synchronization strategies including SSP, BSP, and asynchronous SGD; (iv) AllReduce-based alternatives to the PS paradigm such as Horovod; (v) practical frameworks including TensorFlow, PyTorch Distributed, and Petuum; and (vi) the convergence and correctness trade-offs of relaxed consistency models. The survey will synthesize existing literature, compare design trade-offs across systems, and identify open challenges in parameter synchronization at scale.

---

## Key Topics to be Covered

- Parameter server architecture: server groups, worker groups, scheduler nodes, and the server manager
- Range-based push/pull communication and vectorized (key, value) parameter representation
- Consistency models: sequential (BSP), eventual consistency, bounded delay (SSP), and asynchronous SGD
- Fault tolerance mechanisms: vector clocks, chain replication, and consistent hashing
- AllReduce vs. Parameter Server: communication topology trade-offs
- Gradient aggregation algorithms: distributed subgradient descent and delayed block proximal gradient
- Practical frameworks: TensorFlow, Horovod, PyTorch Distributed, Petuum, DistBelief
- Convergence guarantees and correctness under relaxed consistency

---

## GitHub Repository
All papers, slides, and bibliography are available at:
https://github.com/Suvan8806/CS5463-4953---Scaling-Distributed-Machine-Learning-with-the-Parameter-Server