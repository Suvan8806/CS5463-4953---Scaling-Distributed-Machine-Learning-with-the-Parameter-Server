# Annotated Bibliography — CS 5463/4953 Term Project
## Survey on Distributed Machine Learning: Systems, Algorithms, and Scalability

**GitHub:** https://github.com/Suvan8806/CS5463-4953---Scaling-Distributed-Machine-Learning-with-the-Parameter-Server

---

## Category I: Existing Survey Papers

**[S1]** Verbraeken, J., Wolting, M., Katzy, J., Kloppenburg, J., Verbelen, T., & Rellermeyer, J. S. (2020). A survey on distributed machine learning. *ACM Computing Surveys, 53*(2), 1–33.
https://arxiv.org/abs/1912.09789

> This survey provides a comprehensive overview of distributed ML by organizing the field into three layers: the ML algorithm layer, the parallelism strategy layer, and the network topology layer. It categorizes systems by how they distribute data and computation, covering both synchronous and asynchronous approaches. The paper surveys popular frameworks including TensorFlow, MXNet, and Spark, comparing their design choices and scalability trade-offs. It is particularly useful as a reference for understanding how communication overhead scales with cluster size and model complexity.

---

**[S2]** Ben-Nun, T., & Hoefler, T. (2019). Demystifying parallel and distributed deep learning: An in-depth concurrency analysis. *ACM Computing Surveys, 52*(4), 65:1–65:43.
https://arxiv.org/abs/1802.09941

> This survey approaches distributed deep learning from a concurrency and systems perspective, modeling parallelism at multiple levels — from individual operators to full distributed training pipelines. It provides a formal treatment of data parallelism, model parallelism, and pipeline parallelism, and compares AllReduce versus parameter server communication topologies. The paper also reviews asynchronous SGD variants and discusses how different DNN architectures affect parallelization strategy choices. It stands out for its theoretical grounding alongside practical system comparisons.

---

**[S3]** Mirzadeh, S. et al. (2023). From distributed machine learning to distributed deep learning: A comprehensive survey. *Journal of Big Data, 10*, 148.
https://link.springer.com/article/10.1186/s40537-023-00829-x

> This recent journal survey traces the evolution of distributed ML from classical algorithms like decision trees and SVMs through to modern deep neural networks, covering both data parallel and model parallel strategies. It categorizes distributed deep learning systems by their synchronization mechanisms and communication patterns, and includes coverage of federated learning and reinforcement learning in distributed settings. The survey is notable for its broad scope and for discussing practical deployment challenges such as heterogeneous hardware and network bandwidth constraints.

---

## Category II: Foundational Papers

**[F1]** Smola, A. & Narayanamurthy, S. (2010). An architecture for parallel topic models. *Proceedings of the VLDB Endowment, 3*(1-2), 703–710.
https://dl.acm.org/doi/10.14778/1920841.1920931

> This is the first-generation parameter server paper, introducing a distributed key-value store architecture for synchronizing parameters across machines during LDA topic model inference. Workers update local counts and push them to a shared distributed storage layer without requiring explicit synchronization barriers. The system achieved over an order of magnitude speedup compared to prior single-machine methods for topic modeling. This paper established the core push/pull communication abstraction that all subsequent parameter server designs built upon.

---

**[F2]** Dean, J. & Ghemawat, S. (2008). MapReduce: Simplified data processing on large clusters. *Communications of the ACM, 51*(1), 107–113.
https://dl.acm.org/doi/10.1145/1327452.1327492

> MapReduce introduced the foundational programming model for distributed data processing at Google, abstracting cluster computation into map and reduce operations that the runtime automatically parallelizes and fault-tolerates. While not specific to ML, it became the basis for early distributed ML systems including Mahout and MLbase. The paper's treatment of fault tolerance via task re-execution influenced how later ML systems handle worker failures. Its limitations for iterative workloads — which require repeated passes over data — directly motivated the development of parameter servers and Spark.

---

**[F3]** Dean, J., Corrado, G., Monga, R., Chen, K., Devin, M., Mao, M., ... & Ng, A. Y. (2012). Large scale distributed deep networks. *Advances in Neural Information Processing Systems, 25 (NIPS 2012).*
https://papers.nips.cc/paper/2012

> This paper introduced DistBelief, Google's second-generation parameter server framework specifically designed for deep neural networks. It proposed two training algorithms: Downpour SGD, which allows model replicas to asynchronously push and pull parameters from a sharded parameter server, and Sandblaster L-BFGS for batch optimization. DistBelief was used to train a neural network 100x larger than anything previously reported at the time. The paper is a direct predecessor to the Li et al. OSDI 2014 work and established the idea of using multiple model replicas with a central parameter store.

---

**[F4]** Li, M., Zhou, L., Yang, Z., Li, A., Xia, F., Andersen, D. G., & Smola, A. J. (2013). Parameter server for distributed machine learning. *Big Learning Workshop, NIPS 2013.*
https://www.cs.cmu.edu/~muli/file/ps.pdf

> This workshop paper describes an intermediate version of the parameter server framework that bridges DistBelief and the full OSDI 2014 system. It presents the core (key, value) vector abstraction for parameters and describes the push/pull interface used by workers. The paper outlines convergence guarantees for proximal gradient methods under the asynchronous update model, showing linear scalability on logistic regression tasks with up to 64 billion attributes. It served as a proof-of-concept demonstrating that general-purpose PS systems could handle diverse ML workloads beyond deep networks.

---

**[F5]** Ho, Q., Cipar, J., Cui, H., Lee, S., Kim, J. K., Gibbons, P. B., Gibson, G. A., Ganger, G., & Xing, E. P. (2013). More effective distributed ML via a stale synchronous parallel parameter server. *Advances in Neural Information Processing Systems, 26 (NIPS 2013),* 1223–1231.
https://proceedings.neurips.cc/paper/2013/hash/b7bb35b9c6ca2aee2df08cf09d7016c2-Abstract.html

> This paper introduces the Stale Synchronous Parallel (SSP) consistency model, where workers are allowed to read parameter values that are up to a bounded number of iterations stale rather than always fetching the latest version. The authors prove correctness guarantees for SSP and demonstrate that it outperforms both fully synchronous (BSP) and fully asynchronous schemes on matrix factorization, topic modeling, and Lasso regression. The key insight is that SSP reduces network waiting time substantially while only marginally slowing convergence per iteration, resulting in faster wall-clock convergence overall.

---

**[F6]** Li, M., Andersen, D. G., Park, J. W., Smola, A. J., Ahmed, A., Josifovski, V., Long, J., Shekita, E. J., & Su, B.-Y. (2014). Scaling distributed machine learning with the parameter server. *11th USENIX Symposium on Operating Systems Design and Implementation (OSDI 14),* 583–598.
https://www.usenix.org/conference/osdi14/technical-sessions/presentation/li_mu

> This is the primary reference paper for this survey. It presents the third-generation parameter server framework, introducing range-based push/pull communication over ordered (key, value) vectors to batch parameter updates and reduce network overhead. The system supports flexible consistency models through a tunable delay parameter τ, enabling a spectrum from fully synchronous to fully asynchronous execution. It also introduces vector clocks for tracking parameter freshness, chain replication for fault tolerance, and consistent hashing for parameter distribution. Evaluations on 1000 machines with 636TB of real data show significant speedups over prior systems.

---

**[F7]** Li, M., Andersen, D. G., Smola, A., & Yu, K. (2014). Communication efficient distributed machine learning with the parameter server. *Advances in Neural Information Processing Systems, 27 (NIPS 2014).*
https://proceedings.neurips.cc/paper/2014

> This companion paper to the OSDI 2014 work focuses specifically on reducing communication overhead in parameter server systems through two mechanisms: a significantly modified filter that suppresses gradient updates below a threshold, and a KKT-based filter derived from the optimality conditions of the optimization problem. Together these filters can reduce outgoing network traffic by over 90% without materially degrading convergence. The paper provides convergence proofs for the compressed update scheme and validates it on L1-regularized logistic regression and reconstruction ICA on GPU clusters.

---

**[F8]** Zaharia, M., Chowdhury, M., Das, T., Dave, A., Ma, J., McCauley, M., Franklin, M. J., Shenker, S., & Stoica, I. (2012). Resilient distributed datasets: A fault-tolerant abstraction for in-memory cluster computing. *USENIX NSDI 2012.*
https://www.usenix.org/conference/nsdi12/technical-sessions/presentation/zaharia

> This paper introduced Spark and the Resilient Distributed Dataset (RDD) abstraction, which enables in-memory iterative computation on distributed clusters. Unlike MapReduce, Spark retains intermediate state between iterations, making it far more efficient for ML workloads that require multiple passes over training data. Fault tolerance is achieved through lineage — the ability to recompute lost partitions rather than checkpointing full state. Spark became the foundation for MLlib and influenced how distributed ML systems handle iterative gradient-based optimization.

---

## Category III: Recent Conference Papers

**[C1]** Abadi, M., Barham, P., Chen, J., Chen, Z., Davis, A., Dean, J., ... & Zheng, X. (2016). TensorFlow: A system for large-scale machine learning. *12th USENIX Symposium on Operating Systems Design and Implementation (OSDI 16),* 265–283.
https://www.usenix.org/conference/osdi16/technical-sessions/presentation/abadi

> TensorFlow represents Google's successor to DistBelief, replacing the parameter server model with a dataflow graph abstraction where both computation and shared state are expressed as nodes in a directed graph. This design allows TensorFlow to flexibly map operations across CPUs, GPUs, and TPUs without the tight coupling of the PS architecture. The system supports both synchronous and asynchronous execution through its graph scheduler and was open-sourced in 2015. It introduced the concept of stateful variable nodes that can be updated by multiple workers concurrently, a cleaner abstraction than the sharded PS approach.

---

**[C2]** Sergeev, A. & Del Balso, M. (2018). Horovod: Fast and easy distributed deep learning in TensorFlow. *arXiv preprint arXiv:1802.05799.*
https://arxiv.org/abs/1802.05799

> Developed at Uber, Horovod replaces TensorFlow's parameter server-based distributed training with a ring-AllReduce communication pattern inspired by MPI collective operations. Each GPU communicates only with its neighbors in a logical ring, averaging gradients with optimal bandwidth utilization. The paper shows Horovod achieves 90% scaling efficiency on 128 servers for ResNet and Inception models. A key contribution is Tensor Fusion, which batches small gradient tensors together before the AllReduce to amortize communication startup costs.

---

**[C3]** Li, S., Zhao, Y., Varma, R., Salpekar, O., Noordhuis, P., Li, T., ... & Chintala, S. (2020). PyTorch distributed: Experiences on accelerating data parallel training. *Proceedings of the VLDB Endowment, 13*(12), 3005–3018.
https://arxiv.org/abs/2006.15704

> This paper describes the design of PyTorch's Distributed Data Parallel (DDP) module, which overlaps gradient communication with backward pass computation to hide AllReduce latency. Rather than waiting until all gradients are computed, DDP uses bucketing to begin AllReduce operations as soon as a bucket of gradients is ready. The paper discusses the challenges of gradient ordering, straggler handling, and ensuring consistent bucket assignments across all workers. DDP has become the default distributed training interface in PyTorch and is widely used in both research and production.

---

**[C4]** Rajbhandari, S., Rasley, J., Ruwase, O., & He, Y. (2020). ZeRO: Memory optimizations toward training trillion parameter models. *SC'20: International Conference for High Performance Computing, Networking, Storage and Analysis,* 1–16.
https://arxiv.org/abs/1910.02054

> ZeRO addresses a fundamental limitation of data parallelism: each GPU must store a full copy of model parameters, gradients, and optimizer states, severely limiting model size. ZeRO partitions these three components across GPUs in three progressive stages, reducing memory consumption per GPU proportional to the number of workers. The paper demonstrates training of models up to 170 billion parameters on 400 GPUs with near-linear memory scaling. ZeRO is implemented as part of Microsoft's DeepSpeed library and directly enables the training of modern large language models.

---

**[C5]** Narayanan, D., Shoeybi, M., Casper, J., LeGresley, P., Patwary, M., Korthikanti, V., ... & Zaharia, M. (2021). Efficient large-scale language model training on GPU clusters using Megatron-LM. *SC'21: International Conference for High Performance Computing, Networking, Storage and Analysis,* 1–15.
https://arxiv.org/abs/2104.04473

> This paper shows how tensor parallelism, pipeline parallelism, and data parallelism can be composed together to train models with up to one trillion parameters on thousands of GPUs. The key contribution is an interleaved pipeline schedule that reduces pipeline bubble time by over 10% compared to naive pipeline parallelism. The paper provides a detailed analysis of the communication volume and compute utilization trade-offs of each parallelism type, offering practical guidance on how to configure 3D parallelism for different model sizes and cluster topologies.

---

**[C6]** Li, S. & Hoefler, T. (2022). Near-optimal sparse AllReduce for distributed deep learning. *Proceedings of the 27th ACM SIGPLAN Symposium on Principles and Practice of Parallel Programming (PPoPP '22),* 135–149.
https://arxiv.org/abs/2201.07598

> This paper addresses the scalability problem of sparse AllReduce operations, which arise when gradient sparsification is applied to reduce communication volume. Existing sparse AllReduce algorithms suffer from increasing communication volume as the number of workers grows. The proposed Ok-TopK algorithm achieves asymptotically optimal communication volume of O(k) regardless of the number of processes by combining a novel sparse reduction algorithm with decentralized parallel SGD. Experiments on the Piz Daint supercomputer show that Ok-TopK achieves similar model accuracy to dense AllReduce while significantly reducing communication time.

---

**[C7]** Zhang, L., Zhang, L., Shi, S., Chu, X., & Li, B. (2023). Evaluation and optimization of gradient compression for distributed deep learning. *IEEE 43rd International Conference on Distributed Computing Systems (ICDCS 2023),* 361–371.
https://arxiv.org/abs/2306.08881

> This paper provides a practical evaluation of three representative gradient compression methods — Sign-SGD quantization, Top-k sparsification, and PowerSGD low-rank compression — on a 32-GPU cluster. The results reveal that compression methods often fail to outperform well-optimized dense AllReduce due to incompatibility with key system optimizations like tensor fusion and computation-communication pipelining. The authors propose ACP-SGD, a new alternating compressed Power-SGD method that is compatible with these system optimizations and achieves a 4x speedup over standard synchronous SGD.

---

**[C8]** Agarwal, S., Wang, H., Venkataraman, S., & Papailiopoulos, D. (2022). On the utility of gradient compression in distributed training systems. *Proceedings of Machine Learning and Systems (MLSys 2022).*
https://proceedings.mlsys.org/paper_files/paper/2022/file/773862fcc2e29f650d68960ba5bd1101-Paper.pdf

> This paper critically examines when gradient compression actually helps in real distributed training systems rather than in idealized benchmarks. The authors find that compression benefits are highly sensitive to the network bandwidth regime, the number of workers, and the specific model architecture — and that under high-bandwidth interconnects, compression often provides little benefit due to its computational overhead. The paper introduces a framework for reasoning about when compression is worthwhile and provides practitioners with guidelines for deciding whether to apply it in their specific deployment setting.

---

**[C9]** Xing, E. P., Ho, Q., Dai, W., Kim, J. K., Wei, J., Lee, S., Zheng, X., Xie, P., Kumar, A., & Yu, Y. (2015). Petuum: A new platform for distributed machine learning on big data. *Proceedings of ACM KDD 2015,* 1335–1344.
https://dl.acm.org/doi/10.1145/2783258.2783323

> Petuum is a distributed ML platform built around the SSP consistency model from Ho et al. 2013, extending it with a structure-aware scheduler that exploits the iterative-convergent nature of ML algorithms. Unlike general-purpose distributed systems, Petuum is specifically designed around the observation that ML algorithms can tolerate bounded parameter staleness without diverging. The platform supports a range of ML tasks through a unified interface and demonstrates that structure-aware scheduling can further reduce synchronization overhead compared to naive SSP implementations.

---

## Category IV: Recent Journal Papers

**[J1]** Lian, X., Zhang, C., Zhang, H., Hsieh, C.-J., Zhang, W., & Liu, J. (2017). Can decentralized algorithms outperform centralized algorithms? A case study for decentralized parallel stochastic gradient descent. *Advances in Neural Information Processing Systems, 30 (NIPS 2017).*
https://arxiv.org/abs/1705.09056

> This paper challenges the assumption that centralized parameter server architectures are necessary for distributed SGD, showing theoretically and empirically that decentralized approaches where workers communicate only with neighbors can match or exceed the convergence rate of centralized PS-based training. The key result is that decentralized parallel SGD achieves the same asymptotic convergence rate as centralized SGD under certain conditions, while avoiding the communication bottleneck at the parameter server. This work motivated a line of research into gossip-based and ring-topology distributed training systems.

---

**[J2]** Recht, B., Re, C., Wright, S., & Niu, F. (2011). Hogwild!: A lock-free approach to parallelizing stochastic gradient descent. *Advances in Neural Information Processing Systems, 24 (NIPS 2011),* 693–701.
https://arxiv.org/abs/1106.5730

> Hogwild! demonstrates that SGD can be parallelized on shared-memory systems without any locking mechanisms by simply allowing processors to read and overwrite parameters without synchronization. The key theoretical insight is that when the training data is sparse — meaning each example only touches a small fraction of parameters — the probability of harmful write conflicts is low and convergence is still guaranteed. This work directly influenced the design of asynchronous parameter server systems, showing that relaxed consistency can be theoretically justified for sparse ML problems.

---

**[J3]** Goyal, P., Dollár, P., Girshick, R., Noordhuis, P., Wesolowski, L., Kyrola, A., ... & He, K. (2017). Accurate, large minibatch SGD: Training ImageNet in 1 hour. *arXiv preprint arXiv:1706.02677.*
https://arxiv.org/abs/1706.02677

> This Facebook paper demonstrates that synchronous data-parallel training can be scaled to 256 GPUs with a minibatch size of 8192 while maintaining the same final accuracy as single-GPU training, achieved by linearly scaling the learning rate with batch size. The paper introduces a warmup learning rate schedule to stabilize early training at large batch sizes. Training ResNet-50 on ImageNet in one hour demonstrated that synchronous distributed training, when carefully tuned, can be highly practical — providing an important counterpoint to the asynchronous approaches favored by parameter server designs.

---

**[J4]** Mirzadeh, S. et al. (2023). From distributed machine learning to distributed deep learning: A comprehensive survey. *Journal of Big Data, 10*, 148.
https://link.springer.com/article/10.1186/s40537-023-00829-x

> *(See annotation under Category I — S3 above. Listed here as it also serves as a recent journal reference.)*

---

**[J5]** Shoeybi, M., Patwary, M., Puri, R., LeGresley, P., Casper, J., & Catanzaro, B. (2019). Megatron-LM: Training multi-billion parameter language models using model parallelism. *arXiv preprint arXiv:1909.08053.*
https://arxiv.org/abs/1909.08053

> Megatron-LM introduces intra-layer tensor model parallelism for transformer models, splitting individual matrix multiplications across multiple GPUs using column and row parallel linear layers. This requires only two AllReduce operations per transformer layer — one in the forward pass and one in the backward pass — making it highly communication-efficient compared to naive model parallelism. The approach is implemented entirely in native PyTorch without requiring a new compiler, and scales transformer models to 8.3 billion parameters on 512 GPUs with 76% scaling efficiency.

---

**[J6]** Zinkevich, M., Weimer, M., Li, L., & Smola, A. J. (2010). Parallelized stochastic gradient descent. *Advances in Neural Information Processing Systems, 23 (NIPS 2010),* 2595–2603.
https://proceedings.neurips.cc/paper/2010/hash/abea47ba24142ed16b7d8fbf2c740e0d-Abstract.html

> One of the earliest papers on parallelizing SGD, this work proposes a simple approach where each worker independently runs SGD on its own data partition and the resulting parameter vectors are averaged at the end of each round. Despite its simplicity, the paper provides convergence analysis showing that the averaged model converges at the same rate as sequential SGD in expectation. This "model averaging" approach is the conceptual basis for federated learning and local SGD methods, and represents a key alternative to the gradient-aggregation approach taken by parameter servers.