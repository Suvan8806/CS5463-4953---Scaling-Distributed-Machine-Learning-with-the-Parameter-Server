# CS 5463/4953 – Survey-Based Term Project
## Topic Selection Write-Up
**Date:** March 6, 2026

---

## Survey Title
Survey on Parameter Server Frameworks for Distributed Machine Learning

## Category
Distributed Deep Learning — Parameter Distribution and Synchronization

---

## Problem Statement

As machine learning models continue to grow in scale, training them on a single machine has become computationally infeasible. Modern ML models can require on the order of 10⁹ to 10¹² parameters, demanding systems that can distribute both data and computation across many machines efficiently. A core challenge in this setting is how to manage globally shared model parameters across a cluster of worker nodes — ensuring that updates are communicated efficiently, that the system is fault tolerant, and that consistency between nodes is maintained without becoming a bottleneck to performance. The Parameter Server (PS) framework is the dominant architectural paradigm for addressing this problem, yet the design choices involved — particularly around consistency models, communication efficiency, and fault tolerance — vary significantly across systems and remain an active area of research.

---

## Scope of the Survey

This survey focuses on the Parameter Server framework as an architecture for distributed machine learning, tracing its evolution from first-generation systems to modern implementations. Specifically, the survey will cover: (i) foundational work on parallel and distributed parameter management, including early key-value based approaches; (ii) the core PS architecture — server groups, worker groups, range-based push/pull communication, and flexible consistency models; (iii) alternative synchronization strategies including Bulk Synchronous Parallel (BSP), asynchronous SGD, and Stale Synchronous Parallel (SSP); (iv) practical distributed ML frameworks built on PS principles, including DistBelief and TensorFlow; and (v) evaluation benchmarks and real-world applications including sparse logistic regression, Latent Dirichlet Allocation, and distributed sketching. The survey aims to synthesize existing literature, compare design trade-offs across systems, and highlight open challenges in scaling distributed ML.

---

## Key Topics to be Covered

The survey will cover the following key areas:

- Parameter server architecture: server nodes, worker nodes, scheduler nodes, and the server manager
- Range-based communication: vectorized (key, value) parameters, push/pull operations, and message compression
- Consistency models: sequential (BSP), eventual, bounded delay, and stale synchronous parallel (SSP)
- Fault tolerance mechanisms: vector clocks, chain replication, and consistent hashing
- Gradient aggregation algorithms: distributed subgradient descent and delayed block proximal gradient methods
- Comparison of distributed ML systems: DistBelief, Petuum, TensorFlow, and the Parameter Server
- Applications and benchmarks: sparse logistic regression, LDA topic modeling, and distributed sketching