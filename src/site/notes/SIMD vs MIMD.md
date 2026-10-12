---
{"dg-publish":true,"permalink":"/simd-vs-mimd/","created":"2026-10-12T10:27:36.240+01:00","updated":"2026-10-12T10:49:38.191+01:00","dg-note-properties":{}}
---

#hpc 
The confusion usually comes from the word "Multiple." Multiple *what*? Let's fix that.

###  SIMD: (The Army Drill)
Imagine a drill sergeant yelling at a line of 100 soldiers.
*   **The Instruction:** "Do a push-up!📢"
*   **The Data:** 100 soldiers.

The sergeant gives **ONE instruction**. All 100 soldiers do the exact same thing at the exact same time. There is no confusion. They are all operating in lockstep.

**In Computing:**
You have a list of 1,000 numbers: `[1, 2, 3, 4, 5...]`. You want to add 10 to all of them.
*   The CPU/GPU says: "Add 10" (One instruction).
*   The hardware applies it to all 1,000 numbers simultaneously (Multiple data).
*   **The limitation:** Every single unit must do the *exact same thing*. If Soldier #7 doesn't have arms, he can't do the push-up, but the rest of the line has to wait for him or skip him.

### MIMD: (The Hospital)
Imagine a hospital with 4 different doctors.
*   Doctor 1 is doing surgery on Patient A.🧵
*   Doctor 2 is prescribing medicine to Patient B.💊
*   Doctor 3 is reading an X-ray of Patient C.🩻
*   Doctor 4 is giving a vaccine to Patient D.💉

**Multiple Instructions** (Surgery, prescribing, reading, vaccinating) on **Multiple Data** (Patient A, B, C, D). Every doctor is doing their own completely independent thing. They don't have to wait for each other. 

**In Computing:**
You have a modern 8-core CPU. 
*   Core 1 is calculating a spreadsheet for Excel.
*   Core 2 is rendering graphics for a video game.
*   Core 3 is fetching data from a database.
*   Core 4 is playing Spotify.
*   **The flexibility:** Each core can run a *different* program with *different* instructions. They are totally independent.

### ⚔️ The Ultimate Showdown

| Feature | SIMD | MIMD |
| :--- | :--- | :--- |
| **Instruction Stream** | ONE single instruction broadcast to everyone. | MANY different instructions, one per processor. |
| **Data Stream** | MANY different pieces of data. | MANY different pieces of data. |
| **Execution Style** | Lockstep (all together). | Asynchronous (everyone does their own thing). |
| **Hardware Example** | GPUs, Vector Processors (SSE, AVX), TPUs. | Multi-core CPUs, Clusters, Supercomputers. |
| **Best For** | Repetitive math on huge arrays (Matrix multiplication, image processing). | Complex logic, running many different applications at once, branching code. |
| **Programming Difficulty** | Harder (you have to force your problem into a single-instruction box). | Easier (you just write normal code and the OS spreads it out). |

###  Why This Matters for Your Course
*   **If you want to train a Neural Network (AI):** You use **SIMD** (GPUs/TPUs). You are doing billions of identical matrix multiplications on millions of data points. 
*   **If you are writing an Operating System or a Web Server:** You use **MIMD** (Multi-core CPU). You have to handle a web request, update a database, and manage memory all at the same time. 
* ***

### 1. What is the "Inflexibility" of SIMD?
The inflexibility comes down to one core rule: **Every lane must do the exact same operation at the exact same time.** This causes three specific problems in HPC:

*   **Branching🛣️ (The `if` problem):** If your code has `if (x > 0) { do A } else { do B }`, a CPU core can easily handle it. But SIMD cannot. It has to execute *both* A and B for all lanes, and then use a "mask" to throw away the wrong results. This wastes massive amounts of computing power.
*   **Memory Access 🗃️(Gather/Scatter):** SIMD loves data that is lined up neatly in a row in memory (like an array). If it has to fetch data from random, scattered locations, it becomes extremely slow because it has to "gather" each piece individually before it can do the math.
*   **Data Types📦️:** SIMD units are built to handle specific data sizes (e.g., 32-bit floats). If you have a mix of 8-bit integers, 16-bit integers, and 64-bit doubles, the SIMD unit struggles to pack them efficiently.

### 2. Handicapped Soldier  (Divergence)
This is exactly the branching problem. Let's use a concrete HPC example. 

Imagine you have a massive array of 8 numbers: `[1, 2, 3, 4, 5, 6, 7, 8]`.
Your code says: **"If the number is even, multiply it by 10. If it's odd, leave it alone."**

*   **In MIMD (Multi-core CPU):** You can give the even numbers to Core 1 and the odd numbers to Core 2. Core 1 multiplies them. Core 2 does nothing. Everyone is happy. Fast.⚡️
*   **In SIMD (GPU):** The instruction stream says "Multiply by 10". It broadcasts this to all 8 lanes.
    *   Lanes 1, 3, 5, 7 (the odd numbers) are the "handicapped soldiers." They are forced to do the multiplication (1×10=10, 3×10=30, etc.), even though they don't need to.
    *   Lanes 2, 4, 6, 8 do the multiplication correctly (20, 40, 60, 80).
    *   **The Mask:** After the math is done, the hardware throws away the results from the odd lanes. 

The "handicapped soldier" didn't just stand there and wait. He was forced to do the push-up, and then his work was thrown in the trash. This means the SIMD unit spent 8 clock cycles doing work, but only got 4 useful results. **The efficiency is 50%.** In complex AI models with lots of `if` statements, this "divergence" can severely bottleneck a GPU.
