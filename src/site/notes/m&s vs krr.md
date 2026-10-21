---
{"dg-publish":true,"permalink":"/m-and-s-vs-krr/","created":"2026-10-16T16:50:57.584+01:00","updated":"2026-10-16T16:56:16.982+01:00","dg-note-properties":{}}
---

#ms vs #krr 

 **both courses are about "translating the world for computers."** But they do it for **different purposes** and with **different tools**. Think of it this way:

| | **Représentation des connaissances et raisonnement (KRR)** | **Modélisation et simulation (M&S)** |
|---|---|---|
| **Core question** | "What does the system *know*, and what can it *deduce*?" | "How does the system *evolve over time*, and what happens if we change X?" |
| **Focus** | Symbolic representation + logical inference | Dynamical behavior + numerical prediction |
| **Tools** | Logic (modal, default, description), Bayesian networks, fuzzy sets, belief functions | Differential equations, queueing theory, Petri nets, random number generation, simulation algorithms |
| **Output** | New facts, classifications, decisions based on rules | Predicted trajectories, performance metrics, "what-if" scenarios |
| **Time** | Often static (knowledge base + inference engine) | Inherently dynamic (time-stepped or event-driven) |
| **Typical applications** | Ontologies, multi-agent systems, data mining, image interpretation | Queueing systems, epidemic spread, network performance, industrial optimization |

**The overlap:** Both use probability and uncertainty. KRR uses Bayesian networks to *reason* under uncertainty; M&S uses stochastic processes to *simulate* systems with randomness. Both are AI-adjacent.

**The key difference in one sentence:**
- **KRR** asks: *"Given what I know, what can I conclude?"* (logic, inference)
- **M&S** asks: *"Given how the system works, what will happen next?"* (dynamics, prediction)

You could say KRR is about **knowledge and truth**, while M&S is about **behavior and prediction**. They complement each other: you might use KRR to represent the rules of a system, and M&S to simulate how that system performs over time.

---

