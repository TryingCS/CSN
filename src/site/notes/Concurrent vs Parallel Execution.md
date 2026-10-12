---
{"dg-publish":true,"permalink":"/concurrent-vs-parallel-execution/","created":"2026-10-11T20:47:52.583+01:00","updated":"2026-10-11T21:28:36.611+01:00","dg-note-properties":{}}
---

#hpc 
### **Concept Brief:**  


- **Concurrency** Handling multiple tasks at the same time on a **single processor**. It looks like they are running simultaneously  but only one instruction is executing at any exact nanosecond.

	key techniques: 
		context switching 
		time slicing 
		Scheduling 


    
- **Parallelism (True Simultaneity):** Executing multiple tasks at the exact same time on **multiple processors/cores**. There is no time-sharing required; they are physically running at the same time (like multiple workers building different parts of a car simultaneously).
	-Needs explicit coordination
	key techniques 
		Process coordination
		Shared resources management 

- _Key Takeaway:_ Concurrency is about _dealing with_ many things at once. Parallelism is about _doing_ many things at once.
 ***
 ### Time-Slicing vs. Context Switching

 One is the _strategy_, the other is the _mechanism_.

- **Time-Slicing (The Strategy/Policy):** This is the decision the Operating System makes. It says, _"I will give Application A 10 milliseconds of CPU time. Then I will give Application B 10 milliseconds. Then Application C."_ 
    
- **Context Switching (The Mechanism/Action):** This is the actual physical work required to swap the applications. The CPU has to save all the current data of Application A (its registers, where it was in the code, etc.) to memory. Then it has to load all the saved data of Application B from memory into the CPU's registers. _Then_ it can start running B.
    
    - _Analogy:_ Context switching is Student A packing up their books, Student B sitting down and unpacking their books, and the tutor mentally switching from Algebra to History.
        

**Why it matters:**  
Context switching is **expensive**. It takes time and energy. If you time-slice too frequently (e.g., every 1 millisecond instead of every 10 ms), the CPU spends all its time packing and unpacking books (context switching) and almost no time actually tutoring (executing the program). This is called _overhead_.

**But here's the crucial distinction for your course:**

- **Concurrency (Single Core):** Requires Time-Slicing + Context Switching. It's an illusion.
    
- **Parallelism (Multi-Core):** Does **not** require time-slicing to be simultaneous. If you have 4 cores and 4 applications, each application gets its own physical core. No time-slicing needed. No context switching needed (until you have more tasks than cores).
- 
The slide groups "Scheduling, Time-slicing, Context switching" under Concurrency because those are the _only_ tools a single core has to create the illusion of parallelism. But in true Parallelism, you still have scheduling (managing which thread goes to which core), you just don't need _time-slicing_ to fake simultaneity because you have real physical cores.
***
### 1. "Process coordination" and "Shared resources management"

Are these _parallel-specific_ terms? **No.** They are **Concurrency** concepts that apply to _both_ concurrent and parallel execution, but they get harder in parallel.

- **In Concurrency (Single Core):** You still have multiple software threads/processes. They still need to share the single CPU and the same RAM. The OS must coordinate them. For example, if Thread A is writing to a file while Thread B is trying to read it, the OS needs coordination (like locks or semaphores) so B doesn't read half-written garbage.
    
- **In Parallelism (Multi-Core):** Now the threads are physically running at the exact same time. Process coordination becomes even more critical because you have _true simultaneous_ access to shared memory. If Core 1 and Core 2 try to update the same variable at the exact same nanosecond, you get a "race condition" and corrupt data.
    
- **Shared Resources Management:** In a single core, it's about managing _time_ (who gets the CPU now?). In multi-core, it's about managing _bandwidth_ (who gets to read from RAM now? How do we keep the caches coherent?).
    

**Why the slide lists it under Parallel:** The slide is trying to say that while concurrency _creates_ these problems, parallelism _forces you to explicitly solve them_ in your code (using things like PThreads mutexes or OpenMP critical sections).
![Pasted image ٢٠٢٦١٠١١٢١٢٨٣٥.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A1%D9%A1%D9%A2%D9%A1%D9%A2%D9%A8%D9%A3%D9%A5.png)