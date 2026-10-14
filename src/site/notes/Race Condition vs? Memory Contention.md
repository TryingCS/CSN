---
{"dg-publish":true,"permalink":"/race-condition-vs-memory-contention/","created":"2026-10-13T18:34:56.112+01:00","updated":"2026-10-13T18:37:37.161+01:00","dg-note-properties":{}}
---

#hpc 
Yes, they absolutely **can and do** happen in the same system. 

you are imagining the "long line" as an orderly queue that *prevents* race conditions. It doesn't. 


**Why doesn't the long line prevent the race condition?**
Because the "line" (memory contention) is managed by *hardware*. The hardware ensures that if two cores try to read the same memory address at the exact same nanosecond, one gets to go first. The hardware forces them to take turns *physically accessing the RAM*. 

But the hardware has no idea *what the software is trying to do*. 

### 🏦 The Bank Account Example (The Classic HPC Problem)
Let's make it concrete. You have a variable `balance = 100`. You have two threads running on two different cores. Both threads want to add $50 to the account.
*   **Step 1:** Thread A reads `balance` (100). 
*   **Step 2:** Thread B reads `balance` (100). 
*(Even if they had to wait in line to read due to memory contention, they both get the value 100).*
*   **Step 3:** Thread A calculates 100 + 50 = 150 in its own register.
*   **Step 4:** Thread B calculates 100 + 50 = 150 in its own register.
*   **Step 5:** Thread A writes 150 to memory.
*   **Step 6:** Thread B writes 150 to memory.

**The result:** The balance is 150. It should be 200. That's a **race condition**. 

Notice how the race condition happened because the **read-calculate-write sequence was interrupted**. The hardware line (memory contention) only manages the reading and writing. It doesn't know that Thread A and Thread B are working on the *same logical task*.

### 🔑 The Key Distinction
*   **Memory Contention** is about the **hardware bus/controller** (the physical wire to the whiteboard).
*   **Race Condition** is about the **software logic** (the order of operations across multiple instructions).

You can have:
1.  **High contention, No race condition:** 100 threads all reading the same data (reading doesn't corrupt data).
2.  **Low contention, Race condition:** 2 threads writing to the same variable, but the memory bus is fast so there's no traffic jam. The data still gets corrupted because the logic was wrong.
3.  **Both:** 100 threads all trying to update a shared counter (like a global `sum`). The memory bus is jammed (contention) *and* the final answer is wrong (race condition).

### 🛠️ How HPC Fixes This
This is exactly why, when you write OpenMP or PThreads code later, you will use **locks (mutexes)** or **atomic operations**. 
You are telling the software: *"Hey, don't just rely on the hardware to line up. I need you to explicitly lock this variable so that only ONE thread can do the read-calculate-write sequence at a time."* 

The lock forces the software to form a *logical* line, which prevents the race condition. 

---
