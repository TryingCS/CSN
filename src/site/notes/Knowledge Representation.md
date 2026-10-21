---
{"dg-publish":true,"permalink":"/knowledge-representation/","created":"2026-10-17T18:44:15.898+01:00","updated":"2026-10-17T18:45:53.497+01:00","dg-note-properties":{}}
---

#krr 

For agents to communicate and be truly intelligent, they need to represent their knowledge and agree on the meaning of messages. 

**What is a Knowledge Representation?**
It is a system that defines a set of symbols and a set of operations on those symbols. 
In AI, a knowledge representation system needs two things:
1.  A **formalism** to represent knowledge.
2.  A **reasoning mechanism** to manipulate it.

The fundamental equation here is: **Knowledge = Information + Semantics** (meaning).

**Newell's Three Levels of Representation:**
Newell defined three levels of how we represent knowledge:
1.  **Knowledge Level:** The most abstract level containing all the knowledge.
2.  **Symbolic Level:** The coding of knowledge into a formal language (e.g., logic, rules).
3.  **Implementation Level:** The internal representation of expressions (data structures like lists, arrays, or tables in a computer).

**Example:**
*   **Knowledge Level📚️:** The agent knows there is a plane from Béchar to Oran on 31-10-2018 at 8h30 costing 7000 DA.
*   **Symbolic Level ✏️(Formal Language/Predicate):** `PrixAvion(Béchar, Oran, 31-10-2018, 8h30, 7000DA)`
*   **Implementation Level🖥️:** A table with 5 columns: departure city, arrival city, date, time, and price.

**Why do we need Reasoning?**
Reasoning allows us to generate new knowledge through **inference**= الاستنتاج. 
We reason to accomplish objectives like:
*   Decision making
*   Testing an argument
*   Verifying a proposition

---

