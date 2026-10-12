---
{"dg-publish":true,"permalink":"/shared-memory-system/","created":"2026-10-12T11:08:17.674+01:00","updated":"2026-10-12T11:32:52.339+01:00","dg-note-properties":{}}
---

#hpc 
Recap:
*   **MIMD:** Multiple cores doing different things.
*   **Memory (RAM) and Caches:** Where data lives.
*   **Threads:** Software tasks running on those cores.

"Shared-Memory Systems"  describes **how those cores talk to each other.** 
***
### 🏢 Shared-Memory Systems: The Shared Whiteboard
Imagine a small office with 4 workers (4 CPU cores). 
*   **Shared Memory:** There is one giant whiteboard in the middle of the room (the RAM).
*   **The Rule:** All 4 workers can see the whiteboard. If Worker 1 writes "X = 5" on the whiteboard, Worker 2 instantly sees it. 
*   **Communication:** They don't need to send emails or walk to another building. They just point at the whiteboard. This makes communication **extremely fast**.
*   **The Catch:** If two workers try to erase and write on the same spot at the exact same time, they ruin the data. (This is called a *race condition*, and it's why OpenMP and PThreads exist—to manage this chaos🏁).

 there are two ways to arrange this shared-memory office:

### 🏠 1. SMP (Symmetric Multi-Processing) - The Small Startup
*   **The Setup:** Everyone is in one small room. There is one giant whiteboard.
*   **The Rule:** It takes the exact same amount of time for Worker 1 to walk to the whiteboard as it does for Worker 4. This is **"Uniform Memory Access."** Everyone is equal.
*   **The Problem:** If you add 20 workers to the room, they will trip over each other trying to reach the whiteboard. The whiteboard becomes a bottleneck. This is called **memory contention**.
*   **Real World:** Your standard laptop or desktop. It has 8 cores, one stick of RAM, and they all share it equally.

### 🏢 2. NUMA (Non-Uniform Memory Access) - The Corporate Campus
*   **The Setup:** The company grew. Now they have 4 separate rooms (Nodes). Each room has its own whiteboard (Local RAM). 
*   **The Rule:** A worker can still read the whiteboards in *other* rooms, but it takes much longer to walk down the hall than to look at their own room's whiteboard. This is **"Non-Uniform Memory Access."**
*   **The Speed Difference:** 
    *   *Local Access:* Fast (my room's whiteboard).
    *   *Remote Access:* Slow (the other room's whiteboard).
*   **The Challenge:** If Worker 1 needs data from Room 2's whiteboard, it's slow. To be efficient, the Operating System tries to keep data close to the worker that uses it the most. If it fails, performance drops. This is called **NUMA locality**.
*   **Real World:** High-end servers and supercomputers. They have multiple CPU sockets (physical chips) on one motherboard, each with its own dedicated RAM.

### 💻 Why This Matters for Your Course (Chapter 2)
When you write OpenMP or PThreads code later, you are writing code for a Shared-Memory system. You won't have to manually send messages between cores. You just write to a variable, and all cores can see it. It's easier to program than Distributed Memory (which we'll see in Step 9). 

But you *will* have to deal with the pitfalls: race conditions (two cores writing at once) and NUMA locality (trying to keep data close to the core that needs it).

---
### Epilogue
Race condition = _wrong answer_. Memory contention = _slow answer_
A worker (CPU core) is physically attached to a specific office (memory controller/socket).
"Can they change what office they belong to?"
- **Hardware (No):** A CPU core is soldered to a specific socket. It cannot move.
- **Software (Yes):** The Operating System can _move the data_ (the variables). It can take a page of memory from Office 2 and copy it to Office 1 so the worker in Office 1 can access it faster. This is called **Page Migration**. It can also move a software thread from one core to another, but the core itself stays put.
Even if you don't have a supercomputer, most modern consumer CPUs (like AMD Ryzen or Intel Core i9) are internally NUMA. They have multiple "chiplets" (mini-offices) on the same chip. The Operating System sees them as NUMA nodes.  
When you write OpenMP code later, you will run it on your laptop. It will be a mix of SMP and NUMA. You won't have to manually manage the offices, but the OS and your code's performance will depend on how well they cooperate (a concept called _NUMA locality_).
***
UMA is simple but bottlenecked. NUMA is complex but scalable.
***
The whiteboard represents **Main Memory (RAM)**.  
Variables (integers, arrays, structs) are the _things you write on the whiteboard_. When you write `int x = 5;` in C, you are literally telling the CPU to write the number 5 on a specific spot on the whiteboard. So yes, in your practical work, every variable you share between threads is a spot on that whiteboard.
***
- **Race Condition:** "Worker A and Worker B both tried to write their name on the same line at the same time. The paper is ruined. The answer is wrong." (You fix this with locks/mutexes).
    
- **Memory Contention:** "Ten workers are all crowded around the whiteboard, waiting their turn to read. The answer will be correct, but it's taking forever." (You fix this with better data locality).