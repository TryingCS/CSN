---
{"dg-publish":true,"permalink":"/programming-models-and-interfaces/","created":"2026-10-13T19:13:38.585+01:00","updated":"2026-10-13T19:26:16.310+01:00","dg-note-properties":{}}
---

#hpc 

---

This the "translation layer." It connects the hardware architectures we just discussed to the actual code you will write.

*   **[[Shared-Memory\| Shared Memory]] (SMP/NUMA):** You use **OpenMP** (pragma-based directives, very easy to use) or **PThreads** (low-level API, very explicit and powerful, but harder). 
*   **[[Distributed-Memory Systems\|  Distrubuted Memory]] (Clusters):** You use **MPI** (Message Passing Interface). It's the industry standard for supercomputers. You have to explicitly send and receive messages.
*   **[[Accelerated Systems (Heterogeneous)\| Accelerate Systems]] (GPUs/TPUs):** You use **CUDA** (NVIDIA-specific, highly optimized), **OpenCL** (portable across vendors, but more complex), or **HIP/SYCL** (vendor-neutral).

### **How to choose a model🤏
*   **Architecture Considerations:** What is your hardware? Shared memory (OpenMP) is for fine-grained parallelism and tight coupling. Distributed memory (MPI) is for large-scale problems that exceed one node's capacity.
*   **Application Requirements:** Problem size, data movement overhead, development complexity, and the trade-off between performance and portability.

***
MPI (Message Passing Interface) is the only model in that list designed for **distributed memory**. When you have 500 servers, each with its own independent RAM, there is no shared whiteboard. The nodes must explicitly send messages to each other over the network to coordinate the simulation. OpenMP and PThreads are for shared-memory systems (one computer), and CUDA is for GPUs.