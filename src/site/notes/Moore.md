---
{"dg-publish":true,"permalink":"/moore/","created":"2026-10-14T19:54:06.375+01:00","updated":"2026-10-14T20:07:14.449+01:00","dg-note-properties":{}}
---

#hpc 

For 30 years, these two laws worked in perfect harmony.

- Moore's Law gave us more transistors.
    
- Dennard Scaling let us shrink those transistors, increase the clock speed, and keep the power density stable.
    
- **Result:** Every 2 years, computers got smaller, denser, faster, and stayed cool. Clock speeds went from 10 MHz to 3+ GHz. This was the golden era of single-core performance.
    

### 🧱 The End of Dennard Scaling (Mid-2000s)

Around 2005, transistors got so small (atomic scale) that they started **leaking electricity** (quantum tunneling). They couldn't hold a "0" without leaking power.

- Dennard Scaling broke.
    
- Engineers could no longer increase the clock speed without power density skyrocketing and melting the chip.
    
- **But Moore's Law kept going.** We could still pack more transistors on a chip.
    

### 🚀 The Modern Era (Multi-core)

Since we can't make one core faster (Dennard is dead), what do we do with all the extra transistors Moore's Law gives us?

- **We build more cores.**
    
- Instead of one chef running at 5.0 GHz, we build 8 chefs running at 3.0 GHz.
    
- This is why parallel computing is mandatory today, not just a niche academic topic.
***

*   **Moore's Law = The "What" (The Destination).** It's about *quantity* (density).
*   **Dennard Scaling = The "How" (The Vehicle).** It's about *efficiency* (shrinking + voltage).

### 1. "People were doubling before it. Was it just that we're moving fast?"
.Moore's genius wasn't just "noticing we are moving fast." It was predicting that this rate would be **sustainable and predictable** (roughly every two years) for the foreseeable future. 

It became a **self-fulfilling prophecy**. The entire semiconductor industry (Intel, AMD, TSMC) used Moore's Law as a literal business roadmap. 

### 2. "Was he just talking about adding more transistors on the same chip regardless of shrinking? Is it about chip size?"
**No.** Moore's Law is about **density**, not physical chip size. 

If you want to double the transistors on a chip, you have two options:
1.  Make the physical chip twice as big (a pizza box).
2.  Keep the chip the same size, but make the transistors smaller so they fit twice as densely.

Option 1 is terrible for manufacturing. Larger chips are astronomically more expensive because the odds of a microscopic defect ruining the whole chip skyrocket (the yield problem). So, the industry pursued Option 2. Moore knew this. His original paper explicitly predicted that transistor dimensions would shrink. **Shrinking was the engine that made Moore's Law possible.**

### 3. "Did Dennard just formalize the shrinking guidelines?"
**Yes. Exactly.** 

Moore said, "We are going to pack twice as many transistors on a chip every two years." 
But if you just shrink transistors without changing anything else, they will melt. The electric field inside them gets too strong, they leak electricity, and they destroy themselves.

Dennard (and his colleagues) came in and said: *"Here is the physics-based rulebook on how to shrink them safely."*

### 4. "Is Dennard less about shrinking and more about adjusting the voltage?"
It's both. They are inseparable. Dennard's rule is about the **relationship** between physical size and voltage.

Here is the actual recipe (Dennard Scaling):
*   Shrink the transistor dimensions by a factor of \( \kappa \) (e.g., 30% smaller).
*   **You MUST also shrink the voltage by the same factor \( \kappa \).**
*   If you do this, the power density (heat per square mm) stays constant. The transistor switches faster, uses less energy, and doesn't melt.

If you shrink the transistor but *don't* lower the voltage, the electric field becomes too intense, the transistor breaks down, and it leaks massive amounts of power. So Dennard wasn't "less about shrinking." He was about the **exact mathematical relationship** between shrinking the size and lowering the voltage to keep the chip safe.

### 🍕TL;DR

*   **Moore's Law (The Goal):** The number of transistors on a chip doubles roughly every two years. It's about *quantity* and *density*, not speed. It became the industry's self-fulfilling roadmap.
*   **Dennard Scaling (The Recipe):** The rulebook for how to shrink transistors. If you shrink the dimensions, you *must* proportionally shrink the voltage. This keeps power density constant, allowing clock speeds to increase without melting the chip.
*   **The Golden Era:** Moore provided the density. Dennard provided the efficiency. Together, they gave us 30 years of free speedups (faster clock speeds every year).
*   **The End (Mid-2000s):** Transistors got so small they leaked electricity (quantum tunneling). Dennard Scaling broke. We could no longer lower the voltage to keep them cool. Clock speeds plateaued. 
*   **The Modern Era (Multi-core):** Moore's Law continues (we can still pack more transistors), but Dennard is dead (we can't make them faster). So, we use those extra transistors to build **multiple cores** (parallelism).

---

 you were trying to figure out where "shrinking" belonged. It belongs to both: Moore predicted it would happen to achieve density, and Dennard gave the mathematical rules for doing it without melting the chip. 
