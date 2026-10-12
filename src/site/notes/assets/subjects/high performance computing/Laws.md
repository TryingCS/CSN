---
{"dg-publish":true,"permalink":"/assets/subjects/high-performance-computing/laws/","created":"2026-09-18T08:23:22.247+01:00","updated":"2026-10-12T10:04:42.247+01:00","dg-note-properties":{}}
---

#hpc 
*Moore/[[Dennard scaling\|Dennard scaling]] (Hardware trends⚙️) 
-explain why we were forced to build multi-core chips.


*Amdahl/Gustafson (Software math laws):
-explain how ==much== benefit we can ==actually== get from those chips.
conservative vs. ambitious
***
Amdahl's Law : the maximum speedup of a program is strictly limited by its **sequential fraction** (the parts of the code that _cannot_ be parallelized).
***
[[Gustafson's Law\|Gustafson's Law]] is optimistic: it assumes that when you get a bigger computer, you want to solve a _bigger_ problem
***
![Pasted image ٢٠٢٦١٠١٢٠٩٥٦٣٣.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A1%D9%A2%D9%A0%D9%A9%D9%A5%D9%A6%D9%A3%D9%A3.png)