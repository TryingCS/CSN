---
{"dg-publish":true,"permalink":"/accelerated-systems-heterogeneous/","created":"2026-10-13T18:59:15.444+01:00","updated":"2026-10-13T19:20:42.627+01:00","dg-note-properties":{}}
---


#hpc 
CPU (few smart cores) 🧠
GPU (thousands of simple cores)💪
**Accelerated Systems** :combining them into one machine🚀

### Core Concept
Heterogeneous computing. You have a CPU (the manager) and one or more Accelerators (the specialized workers). 
### The Gotcha🪤
The CPU and the GPU have **distinct, separate memory spaces**. The CPU has your regular RAM. The GPU has its own dedicated VRAM. They cannot directly read each other's memory!
### The Solution
"Offload models." You have to explicitly copy data from the CPU's RAM to the GPU's VRAM over a slow bus 🚌⏳️ (PCIe). The GPU crunches the numbers, and then you copy the result *back* to the CPU. This data movement is expensive and often the bottleneck.
#### Programming Models 
    *   **CUDA:** NVIDIA-specific GPU programming.
    *   **OpenCL:** Portable across different vendors.
    *   **HIP/SYCL:** Vendor-neutral approaches.

#### The Three Types of Accelerators

1.  **CPU-GPU Hybrid:** The standard setup. GPU handles massively parallel computations (Graphics, ML/DL, simulations). CPU handles control flow and sequential tasks. Often uses "Unified Memory" now to hide the copy overhead.
2.  **TPUs (Tensor Processing Units):** Google's custom ASICs. Specialized for ML workloads. High-bandwidth memory. Designed specifically for high-throughput matrix operations (neural networks). 
3.  **Domain-Specific (ASICs):** Tailored for one specific task. DSPs (Signal processing), AI inference chips, Cryptography accelerators. (You'll learn more about these in Chapter 4).

***
That is exactly why NVIDIA is 💰️. They don't just sell the GPU; they sell the entire ecosystem (CUDA, NVLink, the software stack) that makes the CPU-GPU handoff as fast as possible. Everyone needs the CPU for the logic, but the GPU is where the heavy AI math happens. If you can optimize that data transfer (the PCIe bottleneck), you win.
***
next :  [[Programming Models and Interfaces\|Programming Models and Interfaces]]