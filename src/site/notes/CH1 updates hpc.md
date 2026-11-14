---
{"dg-publish":true,"permalink":"/ch-1-updates-hpc/","created":"2026-10-29T19:37:23.252+01:00","updated":"2026-10-29T19:50:15.080+01:00","dg-note-properties":{}}
---

#hpc 
***

the new slides add a lot of specific **new terminology and frameworks**

### 1. The von Neumann Baseline 
We talked about the CPU, but we didn't explicitly name the **von Neumann architecture**. The slide points out that the traditional model has a Control Unit fetching one instruction at a time and one Data stream (SISD). This is the baseline that parallel computing had to break away from.

### 2. The Four Eras Timeline 
The slide includes a fantastic timeline of processor evolution:
*   **Golden Age (1971-1993):** Clock speeds went from 0.74 MHz to 66 MHz. Faster every year, for free.
*   **Clock Race (1997-2004):** Clock speeds hit 3.8 GHz (Pentium 4). This is where the **Power Wall** was hit. 
*   **Multi-core (2005-2016):** The clock speed *dropped* (3.2 GHz to 2.2 GHz), but cores went from 2 to 24. 
*   **Many-core (2017-Today):** Clocks are 2.4-5.7 GHz, but cores are up to 96 (and transistors up to 134 Billion). 

### 3. The "Three Walls" 
Last year, we just said "End of Dennard Scaling = Power Wall." This year, the slides explicitly break the end of single-core scaling into **three distinct walls** that all hit around 2005. You need to know these for the TW:
*   **The Power Wall:** Faster clocks require higher voltage, so power grows like \(f^3\) (a 20% clock increase means a 73% power increase). Clocks stalled at 3-4 GHz. *Solution: More, slower cores.*
*   **The Memory Wall:** The CPU got faster (~50% per year), but DRAM latency barely improved (one access takes ~100 ns, or ~300 cycles). A faster clock just waits faster. *Solution: Hide the latency (caches, many threads, GPUs, NUMA).*
*   **The ILP Wall (Instruction Level Parallelism):** A single instruction stream has too little parallelism. The core runs independent instructions in parallel *by itself* (Superscalar, Out-of-Order), but dependencies and branches limit it to 1-2 instructions per cycle. 
    *   *Pollack's Rule:* 2x the hardware \(\approx\) 1.4x the speed. 
    *   *Solution: Explicit parallelism written by the programmer.*

### 4. The SIMD Sub-categories 
We skipped the three specific types of SIMD architectures that Flynn originally proposed (but are in the TW):
1.  **Array Processor (Now SIMT):** Each unit has separate memory/registers (Modern GPUs).
2.  **Pipelined Processor:** Read data from central resource, process fragments, write back (Vector processors).
3.  **Associative Processor:** Broadcast instruction, each unit makes an independent decision by comparing local data (Content-addressable memory).

### 5. New Hardware Terms 
*   **Lithography🖨️:**  The printing process used to manufacture ICs. It relates to Moore's Law because better lithography (shorter wavelengths) allows smaller transistors.
*   **FSB (Front-Side Bus) and QPI (QuickPath Interconnect):** These are in the TW (Q5 & Q6). The FSB is the old way CPUs communicated with the Northbridge/Memory. QPI is Intel's modern point-to-point interconnect (replacing FSB) to reduce the **Memory Wall**. (This isn't explicitly in the slides, but it's in the TW, so the professor expects you to know it).
*   **Programmer's Responsibility (Slide 11):** Decomposition, Communication/Synchronization, Load Balancing, Race Conditions, Deadlocks. (We discussed these, but the slide formalizes them).

### 6. The Modern Supercomputer View
The conclusion has a brilliant summary: A modern supercomputer is a **MIMD machine with SIMD inside**. 
*   *Cluster level:* Distributed memory (MPI).
*   *Node level:* Shared memory (NUMA, OpenMP/PThreads).
*   *Core level:* Vector/SIMD units (AVX, SVE).
*   *Accelerators:* GPU/TPU/NPU (CUDA/OpenCL).

---
