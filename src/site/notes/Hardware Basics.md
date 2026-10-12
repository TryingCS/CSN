---
{"dg-publish":true,"permalink":"/hardware-basics/","created":"2026-09-30T12:15:52.260+01:00","updated":"2026-10-12T11:05:27.768+01:00","dg-note-properties":{}}
---

#hpc 


### **Transistors & Logic** 💡
*   **Transistor:** A microscopic electrically controlled switch. Has two states: On (1) or Off (0).
*   **Logic Gates:** Transistors wired together to perform basic boolean logic (AND, OR, NOT).
*   **CPU:** Billions of logic gates organized into:
    *   **ALU (Arithmetic Logic Unit):** Performs math and logic.
    *   **Control Unit:** Directs data flow and instruction execution.
    *   **Registers:** Ultra-fast, tiny memory slots inside the CPU.

**Clock & Time** ⏳️
*   **Clock Speed:** The frequency of the CPU's internal metronome (Hz). The tempo at which operations occur.
*   **Clock Domain:** The localized "world" of a specific component. Transistors have no concept of time outside their domain; they only react to voltage when the clock ticks.
*   **Propagation Delay:** The physical time it takes for electricity to travel through wires and flip transistors. This sets the hard physical limit on maximum clock speed.
*   **Dynamic Frequency Scaling:** Clock speed is not permanently hardcoded. The CPU adjusts it on the fly based on workload and temperature (e.g., dropping to 800 MHz to save battery, boosting to 4.5 GHz for heavy tasks).

**Performance & Architecture**
*   **Performance = Clock Speed × IPC (Instructions Per Cycle).**
*   **IPC:** The amount of work done per clock tick. Increased through architecture, not just faster ticking.
*   **Pipelining:** Overlapping instruction execution (like an assembly line) so different stages of multiple instructions run simultaneously.
*   **Superscalar Execution:** Having multiple ALUs so several independent instructions can execute in the exact same clock tick.
*   **Out-of-Order Execution:** Doing independent work while waiting for slow memory operations to finish.
*   **Branch Prediction:** The CPU guesses the outcome of an `if` statement to keep the pipeline full.
    *   *Correct guess:* Zero time lost.
    *   *Misprediction:* The pipeline is flushed. All speculative work is thrown away, wasting clock cycles.
*   **Cache (L1, L2, L3):** Small, very fast memory located close to the CPU to avoid the massive latency of going to RAM.

### **Hardware Reality & Limits**
*   **Dennard Scaling (Ended mid-2000s):** Shrinking transistors no longer kept power density constant. Increasing clock speed caused exponential heat and power consumption.
*   **The Wall:** Engineers could not crank clock speed higher without melting chips.
*   **The Solution:** Stop increasing single-core clock speed. Instead, add multiple processing units (Cores) to the same chip -> **Parallel Computing**.
*   **Transistor Failure:** A dead transistor usually breaks logic, crashing the machine, rather than just slowing it down. 
*   **Binning:** If a transistor in a multi-core chip is defective, manufacturers disable that core and sell the chip as a lower-tier model (e.g., an 8-core chip with one dead core becomes a 7-core chip).

---

### ⚔️ CPU vs. GPU: The Fundamental Difference

A CPU and a GPU are both processors made of transistors, but they are designed with **opposite philosophies**:

**1. The CPU (The "Jack of All Trades")**

- **Design Goal🎯:**  **Latency.** It wants to finish a _single_ task as fast as humanly possible.
    
- **Architecture:** It has a few very powerful cores (e.g., 8 to 16). Most of the chip's real estate is dedicated to Control Units (Branch Prediction, Out-of-Order Execution) and massive Caches (L1, L2, L3).

- **Analogy:** A team of a few brilliant PhDs. If you give them a complex, branching problem (like running an Operating System or a game), they will solve it incredibly fast. But they can only work on a few things at a time.
    
- **[[assets/subjects/high performance computing/Flynn’s Taxonomy\|Flynn’s Taxonomy]]:** MIMD (Multiple Instruction, Multiple Data).
    

**2. The GPU (The "Army of Workers")**

- **Design Goal:** **Throughput.** It wants to do _millions_ of simple tasks simultaneously. It doesn't care if a single task takes slightly longer, as long as it gets through a massive pile of work.
    
- **Architecture:** It has thousands of tiny, simple cores (e.g., 10,000+). Almost no space is wasted on Branch Prediction or huge caches. The transistors are dedicated almost entirely to raw math units (ALUs).
    
- **Analogy:** An army of thousands of high-school math students. If you ask them to solve a single complex differential equation, they will be slow. But if you give them a million simple additions (like matrix multiplication for AI), they will destroy the PhDs.
    
- **Flynn's Taxonomy:** SIMD or SIMT (Single Instruction, Multiple Data/Threads).
    

**How they work together (Heterogeneous Computing):**  
You don't choose one or the other. You use both. The CPU acts as the "manager" (handling logic, I/O, and sequential tasks) and offloads the heavy, repetitive math to the GPU. This is exactly what happens when you train a neural network in PyTorch—the CPU handles the Python script and data loading, while the GPU does the matrix multiplications.

_(This directly answers your Tutorial Sheet Exercise 1.1, Question 4. If you are doing ML/DL, you prioritize a powerful GPU with a decent CPU, because the GPU does the heavy lifting)._
***
### Nvidia 💰️

 SIMD is inflexible and terrible at branching (the `if` problem). Yet, GPUs (which are massive SIMD machines) are the undisputed kings of AI right now. How does that make sense?

The answer: **AI workloads are the absolute perfect match for SIMD, despite its inflexibility.**

Here is why:

 🧠 1. AI is Just Massive Matrix Multiplication
When you train a neural network, what is actually happening under the hood? It's not a bunch of complex `if/else` logic. It's essentially this: 
*   Take a giant grid of numbers (weights).
*   Take another giant grid of numbers (inputs).
*   Multiply and add them together.
*   Repeat a billion times.

There are **almost no branches** in the core math of a neural network. It's just endless, repetitive, identical math on massive arrays of data. This is SIMD's dream. SIMD is inflexible, but if your problem is uniformly "do this exact same math on 10 million numbers," inflexibility doesn't matter. It's pure speed.


🛡️ 2. The "SIMT" Secret (NVIDIA's Trick)
Technically, NVIDIA GPUs aren't pure SIMD. They use a concept called **SIMT (Single Instruction, Multiple Threads)**. 

Here's the trick: When you write CUDA code (which you will do in Chapter 3), you write it like normal MIMD code. You write code for *one* thread, and you pretend that thread has its own independent data. 

But under the hood, the GPU hardware groups threads into "warps" (usually 32 threads). If all 32 threads in a warp hit an `if` statement and take the same path, it's perfect SIMD. If they diverge (some take `if`, some take `else`), the hardware uses a mask, makes them execute both paths, and throws away the wrong answers. 

The programmer gets the *ease* of MIMD programming, but the hardware gets the *efficiency* of SIMD.

 3. The Handicapped Soldier in AI
Even though AI has very few branches, some do exist. The most common one is the **ReLU activation function** (`if x < 0, return 0, else return x`). 

You might think this would cause the "handicapped soldier" problem. But it's actually a very cheap branch. The GPU can just use a simple mask: `x = max(0, x)`. It doesn't stall the pipeline. 

### ⚔️ The Modern Reality (CPU + GPU)
This is why modern AI systems use **both**:
*   **The CPU 🧠 (MIMD):** Handles the complex logic, the `if` statements, the data loading, the operating system, and coordinating the whole training process. It's the general.
*   **The GPU💪 (SIMT/SIMD):** Does the heavy lifting. It takes the massive, uniform matrix math and crunches it at lightning speed. It's the muscle. 

So yes, GPUs are the hot thing for AI *because* AI is almost entirely SIMD-friendly math. If AI required lots of complex branching logic, GPUs would be terrible at it. 

---
