---
{"dg-publish":true,"permalink":"/gustafson-s-law/","created":"2026-10-12T09:48:41.654+01:00","updated":"2026-10-12T09:55:20.753+01:00","dg-note-properties":{}}
---

#hpc 
### Gustafson's Law (Scaled Problem):  

- _Gustafson asks: "How much MORE work did we get done in the same amount of time?"_
### 🔢 Why the formula is:  
==**speedup=S+P×NS+P×N**==
Let's look at the formula from the perspective of **what happens in that fixed 1 hour**.
	
Let's say the total parallel execution time is **1 hour**.

- **S:** The fraction of that hour spent doing sequential work. (e.g., 10% of the hour = 0.1 hours). This is done by 1 chef.
    
- **P:** The fraction of that hour spent doing parallel work. (e.g., 90% of the hour = 0.9 hours).
    

Now, imagine you only had **1 chef** doing the _same amount of scaled work_. How long would it take him?

- The sequential work would still take 0.1 hours.
    
- The parallel work would take **N times longer** because he's alone. So, 0.9×10=9 hours.
    
- **Total time for 1 chef to do the scaled work = 0.1 + 9 = 9.1 hours.**
    

Now, calculate Speedup ![Pasted image ٢٠٢٦١٠١٢٠٩٥٣٣٣.png\|169](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A1%D9%A2%D9%A0%D9%A9%D9%A5%D9%A3%D9%A3%D9%A3.png)
	

![Pasted image ٢٠٢٦١٠١٢٠٩٥٤١١.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A1%D9%A2%D9%A0%D9%A9%D9%A5%D9%A4%D9%A1%D9%A1.png)

Notice how we got that?

![Pasted image ٢٠٢٦١٠١٢٠٩٥٤٥٠.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A1%D9%A2%D9%A0%D9%A9%D9%A5%D9%A4%D9%A5%D9%A0.png)

**That is why we multiply by N.** It calculates how much longer the parallel part would have taken if you only had 1 processor.