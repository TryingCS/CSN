---
{"dg-publish":true,"permalink":"/distributed-memory-systems/","created":"2026-10-13T18:46:02.223+01:00","updated":"2026-10-13T19:00:19.399+01:00","dg-note-properties":{}}
---

#hpc 
next: [[Accelerated Systems (Heterogeneous)\|Accelerated Systems (Heterogeneous)]]
****
### Architectural map🗺️
Remember the office with the shared whiteboard? Imagine the company exploded in size. They are no longer in one building. They are now in **10 separate buildings across the city** (Distributed Memory).

*   **Core Concept:** Each building (Node) has its own workers (CPUs) and its own private whiteboard (Local RAM). 
*   **The Catch:** No one can see another building's whiteboard. There is **no shared memory space**.
*   **Communication:** If Worker A in Building 1 needs data from Building 2, he can't just walk over and read it. He has to send a **message** over the network (like an email or a phone call). This is why it's called **Message Passing**.✉️
*   **The Cost:** Sending a message over the network is *drastically* slower ⏳️than reading from your own local RAM. 
*   **The Programming Model:** You write code using **MPI (Message Passing Interface)**. You have to explicitly tell the program: "Send this array from Node 1 to Node 2."

**Examples of Distributed Systems:**
*   **HPC Clusters:** A room full of computers connected by high-speed cables (InfiniBand).
*   **Cloud Computing:** AWS, Azure, Google Cloud.
*   **Supercomputers:** Fugaku, Summit (thousands of nodes working together).
*   **Grid Computing:** Geographically dispersed resources (like the WLCG for particle physics).
***
### Feels too simple?
The reason you don't have questions right now is that the core concept of Distributed Memory is deceptively simple: *"There is no shared whiteboard. If you want data from another building, send an email."* 

That's it. That's the whole architecture. No race conditions on the hardware level (no shared memory to corrupt). No cache coherence issues. Each node is an independent island. 

**But The *implementation* of that simple concept is a nightmare. 

The slide says "Network communication for collaboration" like it's no big deal. But in Chapter 2 (when you start writing actual MPI code), you will hit the gotchas:

1.  **The Latency Wall⏳️:** Sending an email is fast for a human, but for a CPU, it's an eternity. If your nodes spend all their time sending messages instead of calculating, your supercomputer will be slower than a laptop. You have to design your algorithms to minimize communication.
2.  **Deadlock🔒️:** Node 1 is waiting for a message from Node 2. Node 2 is waiting for a message from Node 1. Nothing happens. The program hangs forever. (This is the #1 bug in MPI programming).
3.  **Data Distribution📦️:** Who decides which node gets which part of the data? If you split it poorly, Node 1 finishes in 1 second, and Node 9 takes 10 hours. The whole cluster waits for the slowest node. 
4.  **Fault Tolerance❎:** If you are running on 10,000 nodes, one *will* fail. What happens to the simulation? Do you start over? Do you save checkpoints?
5.  **Programming Complexity💢:** In OpenMP (shared memory), you just put `#pragma omp parallel for` and the compiler does the magic. In MPI, you have to manually write `MPI_Send` and `MPI_Recv`, manage data types, and explicitly tell every node its "rank" (ID number). It's back to low-level C programming.
