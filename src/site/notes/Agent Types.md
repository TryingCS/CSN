---
{"dg-publish":true,"permalink":"/agent-types/","created":"2026-10-17T18:22:07.555+01:00","updated":"2026-10-17T18:29:08.475+01:00","dg-note-properties":{}}
---

#krr 

The ultimate goal of AI is to design a program that implements the **agent function** (the mapping from perceptions to actions). 
 fundamental equation: **Agent = Architecture + Program**. 
 The program must be adapted to the physical (or virtual) machine it runs on.

Agents are categorized by how complex their internal decision-making is. They evolve from simple to complex:

**1. Agent Réactif (Simple Reflex Agent)**
*   **How it works:** Acts *only* based on its current perception. It ignores the past (no history, no memory).
*   **Mechanism:** Condition-Action rules (e.g., "If condition X is met, do action Y").
*   **Limitation:** It only succeeds if the environment is **completely observable**. If it can't see everything it needs right now, it fails.
*   **Example:** Driving a taxi and seeing the brake lights of the car in front turn on \(\rightarrow\) you immediately brake.

**2. Agent basé modèle (Model-based Agent)**
*   **How it works:** Because the real world is usually partially observable, this agent keeps an internal **state** (it stores its history of perceptions).
*   **Mechanism:** It maintains a "model of the world" (knowledge about how the world evolves independently of the agent). 
*   **Example:** If you blink and can't see the road for a second, you still know the car in front is there because you have a mental model of the world.

**3. Agent basé but (Goal-based Agent)**
*   **How it works:** The agent has specific **goals** (desirable states) and chooses actions that bring it closer to that goal.
*   **Example:** A cleaning agent has the goal `[recharge]`. It says: "I need to recharge soon, so I will move towards a zone with power outlets." 

**4. Agent basé utilité (Utility-based Agent)**
*   **How it works:** Sometimes goals conflict or there are multiple ways to reach a goal. This agent uses a **Utility function** to measure the "desirability" or satisfaction of a state.
*   **Mechanism:** If multiple actions are possible, it chooses the action with the highest utility.
*   **Example:** The cleaning agent has `Goal 1 = recharge` and `Goal 2 = don't break down`. If the battery is nearly zero, it calculates: `Utility (don't break down) > Utility (recharge)`. Therefore, it stops moving and sends an alarm signal instead of trying to reach the charger.

*(Note: The slides also mention the **Agent Cognitif**, which is the most advanced level, using complex reasoning and learning, but the detailed breakdown stops at Utility-based).*

---

For a simple reflex agent, the conditions are manually hardcoded (usually as simple `if-then` rules). You can think of it as a basic algorithm connected to sensors and actuators.  
However, the distinction in AI is that an "algorithm" could be incredibly complex, whereas a _Simple Reflex Agent_ is strictly defined by its lack of memory. It maps the _current_ percept directly to an action. If you hardcode enough rules, it acts like an algorithm, but it will still fail in partially observable environments because it cannot remember what happened a second ago.