---
{"dg-publish":true,"permalink":"/hpc-tw/","created":"2026-10-14T19:29:06.840+01:00","updated":"2026-10-15T17:40:06.205+01:00","dg-note-properties":{}}
---

#hpc
# TW1
## EX1
**Question 1:** _"Explain two main reasons that necessitated the shift from single-core performance improvements to parallel computing approaches."_ ❓️
***
- What happened to clock speed?💭
    
- What happened to power density and heat?💭
    
- Why couldn't they just keep making one core faster?💭
***
**Answer** :✅

- **Reason 1: The End of Dennard Scaling.** As transistors shrank, they leaked electricity (quantum tunneling), meaning they consumed power even when idle. This caused **power density** (heat per square millimeter) to skyrocket.
    
- **Reason 2: The Thermal/Power Wall.** Because of this skyrocketing power density, engineers could no longer increase **clock speed** (the frequency of the CPU) without the chip overheating and melting. Single-thread performance plateaued.
    
- **The Shift:** Since we couldn't make one core faster, the industry shifted to using the still-shrinking transistors to build **multiple cores** on a single chip, ushering in the era of parallel computing.
***
**Question 2:_"What do you know about Moore's Law and Dennard Scaling? How do they relate to the evolution of computing hardware? How do they apply in our era of multi-core and many-core processors?"_ ❓️
***
1. What are Moore's Law and Dennard Scaling?💭
    
2. How did they drive computing evolution?💭
    
3. How do they apply to modern multi-core processors?💭
***
**Answer** :✅
- **Moore's Law:** An observation (1965) that transistor density doubles roughly every two years. It's about _quantity_, not speed.
    
- **Dennard Scaling:** A rule (1974) stating that as transistors shrink, voltage and power scale down proportionally, keeping _power density constant_. It's about _efficiency_.
    
- **Evolution:** Together, they allowed 30 years of exponential growth: shrinking transistors led to higher clock speeds without overheating.
    
- **Modern Era (Multi-core):** Dennard Scaling ended in the mid-2000s due to leakage currents and heat limits. We can still follow Moore's Law (more transistors), but we can no longer increase clock speed. We use the extra transistors for **more cores** (parallelism) instead of faster single cores.
***
**Question 3:**
> *"In Operating Systems, you used to learn about processes and threads. When checking your CPU specifications, you may have seen terms like 'cores' and 'threads'. What is the difference between software threads and hardware threads (cores)❓️"*

***
**Answer:**✅
*   **Software Thread:** A programming abstraction. A sequence of instructions managed by the OS scheduler. Thousands can exist. They are blind to the physical hardware.
*   **Hardware Thread / Core:** The physical execution unit on the CPU. 
    *   *Physical Core:* The actual silicon (ALU, registers).
    *   *Logical Core (Hardware Thread):* Created by SMT/Hyper-Threading. One physical core presents itself as two logical cores to the OS to hide memory latency.
*   **The Difference:** Software threads are *tasks*; hardware threads (cores) are *workers*. The OS maps software threads onto hardware threads.
for more:[[threads vs threads\|threads vs threads]]
