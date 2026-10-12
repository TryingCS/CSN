---
{"dg-publish":true,"permalink":"/metrics-that-matter/","created":"2026-10-11T19:57:25.869+01:00","updated":"2026-10-12T09:33:06.814+01:00","dg-note-properties":{}}
---

#hpc 
▸  for analyzing and optimizing parallel programs.


- **Time-based Metrics⌚️:** 
- Wall-clock time (total elapsed time),
- Latency (time per operation), 
- Throughput (operations per second).
    
- **Computational Metrics🖥️:** 
- FLOP/s (Floating-point Operations Per Second, measured in Giga, Tera, Peta),
- Bandwidth💼 (Data transfer rate, GB/s).
    
- **Parallel Performance⚡️:**
    
    - **Speedup (S):** 
      ![Pasted image ٢٠٢٦١٠١٢٠٩٣٣٠٦.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A1%D9%A2%D9%A0%D9%A9%D9%A3%D9%A3%D9%A0%D9%A6.png)
        
    - **Efficiency (E):** E=S/NE=S/N (Speedup divided by the number of processors). Ideal efficiency is 1.0 (or 100%).
***
**1. Speedup: "How much faster did it get?"**  
It's a simple ratio. You compare the old sequential time (T1) to the new parallel time (TN).
- It measures the **raw benefit** of parallelizing.
***
**2. Efficiency : "How well did we use the resources?"**  
If I give you 3 processors, you _hope_ to get 3x speedup. But what if you only get 2x speedup?

- S=2S=2, N=3→E=2/3=66%
    
- This tells you: _"You added 3 processors, but 1/3 of their combined power was wasted."_
    
- Why wasted? Overhead. The processors spent time talking to each other, waiting for data, or doing the parts of the code that can't be parallelized.
    
- **Ideal Efficiency is 1.0 (100%)**. In practice, it always drops as you add more processors.
***
