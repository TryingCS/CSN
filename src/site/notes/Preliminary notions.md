---
{"dg-publish":true,"permalink":"/preliminary-notions/","created":"2026-10-14T18:00:09.785+01:00","updated":"2026-10-17T21:59:30.395+01:00","dg-note-properties":{}}
---

#krr 
***
AI and Intelligent Agents
***
#### What is Intelligence and AI?

- **Intelligence (human) :** The cognitive ability to acquire knowledge, understand complex concepts, reason, adapt to new situations, and solve problems. It includes memory, comprehension, reasoning, and adaptability.
    
- **AI (machine):** The science of making machines perform tasks that normally require human intelligence (e.g., understanding language, recognizing images, making decisions).
    
- _History Note:_ The term "AI" was born at the Dartmouth Conference in **1956**, coined by John McCarthy.
    

**: The Core of AI - Intelligent Agents**  
An **Agent** is anything that can perceive its environment through **sensors** and act upon it through **actuators** (effectuators). It can be physical (a robot) or virtual (a software program).

- **Key Properties of an Agent:**
    
    - _Autonomous:_ Acts based on its own experience/state.
        
    - _Flexible:_ Adapts to changes. 💪
        
    - _Proactive:_ Takes initiative to reach its goals. 
        
    - _Social:_ Interacts with other agents.
        
- **The Agent Cycle:** Agent perceives Environment -> Agent acts on Environment -> Repeat. (This loop never truly ends).
    
- **The Vacuum Cleaner Example:** Imagine an AI vacuum in a 2-room house (A and B). It senses if a room is dirty or clean. Its actions are: Move Left, Move Right, Suck, or Do Nothing. Its simple logic: _If current room is dirty -> Suck. Else -> Move to next room._
    

**The PEAS Model & Rationality**   
When designing an agent, you must define **PEAS**:

- **P**erformance measure (How do we know it did well? e.g., clean floor).
    
- **E**nvironment 🌌🏠️(Where does it operate? e.g., rooms A and B).
    
- **A**ctuators (How does it act? e.g., wheels, suction).
    
- **S**ensors 🔎(How does it perceive? e.g., dirt sensor, location sensor).

- **[[Rational Agent\|Rational Agent]]:** An agent that always chooses the action that maximizes its performance measure based on its perceptions and knowledge.
    

**Types of Agents and Environments**

- **[[Agent Types\|Agent Types]] (from simple to complex):**
    
    1. _Simple Reflex:_ Acts only on current perception (If X, do Y).
        
    2. _Model-based:_ Keeps an internal memory of the world.
        
    3. _Goal-based:_ Acts to reach a specific goal.
        
    4. _Utility-based:_ Acts to maximize "happiness/satisfaction" (utility).
        
    5. _Cognitive:_ Can reason, learn, and make complex plans.
        
- **[[Environment Types\|Environment Types]]🌌:** 
- Accessible (full info) vs Inaccessible; 
- Deterministic (predictable) vs Non-Deterministic; 
- Static vs Dynamic; 
- Discrete vs Continuous;
- Single-agent vs Multi-agent.
    

**Knowledge and Reasoning**

- **Knowledge = Information + Semantics (meaning).**
    
- To make agents communicate, they need a **[[Knowledge Representation\|Knowledge Representation]] System** (a set of symbols and operations).
    
- **[[Reasoning\|Reasoning]]:** Generating new knowledge from what you already know.
    
    - _Deductive:_ General to specific (If all humans are mortal, and Socrates is human -> Socrates is mortal).
        
    - _Inductive:_ Specific to general (Looking at a blood sample to generalize about the whole body).
        
    - _Analogical⚖️:_ Comparing two similar situations.
        
    - _By Absurdity❎:_ Proving something is true by showing the opposite leads to a contradiction.
***
### Tools for Knowledge Representation 


**1. Logic (La logique)**  
Logic is the most essential tool in AI. It is a language made of a formalism (alphabet, rules for forming sentences) and a calculation of truth values.

- **Classical Logic:** Based on binary truth (true = 1, false = 0). There is no in-between.
    
- The slides also list other, more advanced logics (which we will study later in the syllabus):
    
    - **Modal Logic:** Introduces operators like "necessary" and "possible" (used for reasoning about beliefs, obligations, etc.).
        
    - **Default Logic:** A non-monotonic logic that allows drawing conclusions by default when there is no contrary information.
        
    - **Description Logic:** A subset of first-order logic used to represent ontologies (structured knowledge) using concepts, roles, and individuals.
        

**2. Semantic Networks (Réseaux sémantiques)**  
This approach uses **graphs** to represent knowledge. It represents concepts as nodes and their relationships/links as edges. (Think of it as a visual map of how ideas connect).

### **Conclusion:**

- AI is about creating agents that can perceive, reason, and act.
    
- Agents need knowledge, which is represented and processed through reasoning.
    
- There are multiple types of reasoning (Deductive, Inductive, Analogical, Absurdity).
    
- Classical and non-classical logics provide the formal frameworks for AI to handle dynamic contexts, uncertainty, and structured knowledge.
***
***
# extra
**1. "Has a partial representation of its environment"**  
It is **generated by the agent itself** based on what it perceives, not just handed to it by us (though we program the _mechanism_ it uses to generate it).  
Because the environment is usually too complex or "inaccessible" (as we will see later), the agent cannot know _everything_. It only keeps a partial, internal model.  
Exactly as you said: it is a translated version of what it perceives, stored in a "language" (data structures, symbols, or variables) that it can manipulate to reason and make decisions. For example, a self-driving car doesn't see the whole city, it only creates a partial representation of the cars immediately around it.
****
**2. "Possesses its own resources"**  
The agent has internal limits and capabilities. These resources can be:

- **Physical**: Battery life🪫, fuel, physical strength💪.
    
- **Computational**: Processing power, memory storage.
    
- **Temporal**: Time limits to act.  
    An agent must manage its own resources. For instance, a robot vacuum has to manage its battery life; if it runs low, it might stop cleaning and go recharge.
***
**3. "Characteristic" vs "Property"**  
In the context of this course, they are essentially used as synonyms to describe the features of an agent. However, grammatically:

- A **characteristic** is a distinguishing feature or quality (e.g., "It is capable of perceiving").
    
- A **property** is often a behavioral trait that can be observed or measured (e.g., "Autonomy", "Flexibility").  
    In the next section, the slides specifically use the word "Propriétés" (Properties) to categorize the agent's behaviors.