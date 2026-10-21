---
{"dg-publish":true,"permalink":"/m-and-s-ch1-system-modeling/","created":"2026-10-16T16:52:05.836+01:00","updated":"2026-10-16T20:33:10.820+01:00","dg-note-properties":{}}
---

#ms

## Introduction: [[Modeling\|Modeling]] Is Already Part of Your Life


**You already model things — every day, without knowing it.**

Examples from the slides:

- Estimating travel time to get somewhere
- Estimating waiting time at a counter
- Judging whether an apartment rental price is fair
- Deciding whether to take a raincoat (predicting if it will rain)

How do you do it? You unconsciously:
1. List all variables (effects) that could influence your answer
2. Eliminate variables that are negligible
3. Quantify the effect of the remaining selected variables

More examples:
- Predicting ideal cooking time based on food composition, weight, oven temperature, air humidity…
- Predicting wind turbine output based on wind speed at 10m/80m, temperature, pressure, humidity…
- Optimizing a chemical reaction based on time and temperature

**Objectives of modeling:**
- Understand which variables influence a quantitative response variable
- Predict response values for new conditions

---
## **Mathematical Modeling vs. Numerical Simulation**

Let's look at the **Knapsack Problem** (Problème du sac-à-dos).

Imagine you are a hiker. You have a bag that can carry a maximum weight of **P = 15 kg**. You have several objects, each with a weight (pipi​) and a utility/importance (uiui​). You must choose which objects to put in the bag to **maximize the total utility** without exceeding the weight limit.

- **Variables:** xi=1 if you put object i in the bag, xi=0 if you don't.
    
- **The Mathematical Model:**
    
    - Maximize: x1u1+x2u2+⋯+xnunx1​u1​+x2​u2​+⋯+xn​un​
        
    - Subject to: x1p1+x2p2+⋯+xnpn≤Px1​p1​+x2​p2​+⋯+xn​pn​≤P
        

This mathematical formulation is the **Model**. It represents the reality of the hiker's problem in abstract equations.

- **The Simulation:** Finding an algorithm (a step-by-step computational method) to solve these equations on a computer, so you can actually get the answer for any set of objects and any weight limit.
tl;dr: 
> Modeling = the abstract representation (equations, rules, diagrams). 
> Simulation = running/experimenting on that representation to predict behavior

---

## Core Definitions

### 1. System

> **System:** A set of elements interacting with each other to achieve an objective.

Key idea from the slides: *"A system is more than the sum of its parts."* The most interesting properties of a system **emerge** from the interaction between its parts — not from the parts alone.

Example: A bank. The elements are clients, tellers, the queue, the service desks. The "waiting time" property doesn't belong to any single element — it emerges from their interaction.

### 2. Model

> **Model:** A simplified representation of the real system (mathematical, graphical, or computer-based).

### 3. Simulation

> **Simulation:** The process of executing the model to observe and analyze the behavior of the system.

---

## [[Types of Systems\|Types of Systems]] 

### Deterministic Systems 

Their evolution is **perfectly predictable**. They depend only on **known factors**, with no randomness.

Example: A physical equation like x(t)=x0​+v⋅t  — if you know the initial position and velocity, you know exactly where the object will be at any time.

### Stochastic Systems

They include a **random part**. They depend on **random, unpredictable factors**.

Example: Client arrivals in a queue. You can't know exactly when the next client will arrive — only the probability distribution (e.g., Poisson).

---

### Discrete Systems🚦

State changes happen at **precise, separated instants**.

Example: A queue — the state (number of people waiting) changes only when someone arrives or someone finishes being served. Between these events, nothing changes.

### Continuous Systems📈

Evolution is described **continuously in time**.

Example: Population growth, water level in a reservoir. The level changes smoothly and continuously.

### Hybrid Systems 🎛️

Combine **both** discrete and continuous aspects.

Example: An autonomous car — the physics of movement is continuous (speed, position), but events like "traffic light turns red" or "pedestrian detected" are discrete.


---
## Dynamic Systems and Complexity

### Dynamic Systems 🕑️📈📉

In science, we model phenomena whose properties **change with time**. These are called **dynamic systems**. Examples from the slides:

- Movement of planets🪐
- Growth of a plant🌱
- Spread of a disease🦠
- Oscillation of a pendulum ![Pasted image ٢٠٢٦١٠١٦١٨٣٠٣٠.png\|39](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A1%D9%A6%D9%A1%D9%A8%D9%A3%D9%A0%D9%A3%D9%A0.png)
- Flow of clients in a bank
- Evolution of a stock price💹

### The Systems Perspective

Representing nature as a **system** means:
- Putting things in context
- Establishing the nature of their relationships

Key idea: *"The most interesting properties of a system emerge from the interaction between the parts. A system is more than the sum of its parts."*

### Complexity Challenges

When humans model complex systems (climate, epidemics), they struggle with:

- **Feedback / retroactions**
- **Delays** (effect is shifted or delayed relative to the action)
- **Non-linearities** (saturations, amplifications)
- **Multivariate aspects** (high dimensionality, hidden variables, exogenous variables)
- **Uncertainty** (noise, lack of predictability)

Humans often make assumptions of **temporal and spatial contiguity** between cause and effect — meaning they assume causes and effects are close in time and space, which is not always true in complex systems.


---

## The 6-Step Iterative Modeling Process

1. **Problem Definition:** What is the objective? What question must we answer?
2. **Conceptual Model Design:**
   - Delimitation of the system (boundaries)
   - Identification of key variables (inputs, outputs, state)
3. **Mathematical Formalization:**
   - Translate the conceptual model into equations (differential, algebraic) or logical rules
   - Choose probability distributions for stochastic models
4. **Numerical Implementation (Coding):**
   - Use a language (Python, R, MATLAB) or specialized software (Simulink)
   - Create the simulation algorithm
1. **[[Verification and Validation\|Verification and Validation]] (V&V):**
   - Check that the model is correctly implemented (verification)
   - Check that the model accurately represents the real system (validation)
6. **Experimentation and Analysis:**
   - Run scenarios
   - Analyze results

This process loops back as needed — if validation fails, you may return to earlier steps.


---

## Modeling Tools🧰

  allow you to represent, analyze, and simulate complex systems. They offer a mathematical and rigorous representation, enabling verifiable analysis. They facilitate understanding, design, and optimization before real implementation.

### 1. Finite State Machines

Represent the **sequential behavior** of a system. Each **state** corresponds to a situation of the system, and each **transition** corresponds to an event. Used for protocol verification, control modeling, or operating logic.

### 2. Markov Chains

Model **random systems** where the future depends **only on the current state** (Markov property). Used in reliability, performance, queueing, stochastic processes.

### 3. Petri Nets

Represent **concurrent, synchronized, or parallel** systems. Composed of **places**, **transitions**, and **tokens**. Allow analysis of liveness, safety, and reversibility of a system.

### 4. Queueing Models

Model systems where customers/clients arrive, wait, and are served. Used in the bank example from earlier. Help estimate waiting times, utilization rates, and probabilities of excessive waiting.

---

### Numerical Implementation = Coding

Yes, exactly. The slides say: *"Use a language (Python, R, MATLAB) or specialized software (Simulink). Create the simulation algorithm."* 

The word "numerical" here means: you are implementing numerical methods (algorithms that compute numbers) to solve your mathematical model on a computer. It's not just "writing code" in the abstract — it's specifically coding the numerical solution to your equations.

And you're right about validation not being in the analysis phase. The whole point is: you **validate before** you trust the results. If you waited until after running all your scenarios to check if the model is valid, you'd have wasted all that time on potentially meaningless results.

---

### Where Do the Modeling Tools Fit in the 6 Phases?

Great question. The modeling tools (FSM, Markov chains, Petri nets, queueing models) are primarily used in **Step 2 (Conceptual Model Design)** and **Step 3 (Mathematical Formalization)**.

Here's how it works:

**Step 2 — Conceptual Model Design:**
You choose the right tool based on the nature of your system:
- Sequential behavior? → **Finite State Machine**
- Random system with memoryless property? → **Markov Chain**
- Concurrent/parallel processes? → **Petri Net**
- Arrival/waiting/service system? → **Queueing Model**

**Step 3 — Mathematical Formalization:**
You formalize the model using the mathematics of that tool:
- FSM → state transition tables/diagrams
- Markov Chain → transition probability matrix
- Petri Net → incidence matrix, marking equations
- Queueing Model → Kendall notation (e.g., M/M/1), balance equations

**Step 4 — Numerical Implementation:**
You code the simulation algorithm. If you chose a Petri net, you might use CPN Tools. If you chose a queueing model, you might write Python code to simulate arrivals and services.

**Step 6 — Experimentation:**
You run scenarios and analyze results. The tool choice influences what you can analyze (e.g., Petri nets let you check liveness and safety; Markov chains give steady-state probabilities).


# Recap 📝

**1. Modeling is already part of your life**
- You list variables, eliminate negligible ones, quantify the rest
- Goal: understand influences and predict outcomes

**2. Core definitions**
- **System:** elements interacting to achieve an objective (more than the sum of its parts)
- **Model:** simplified representation (mathematical, graphical, or computer-based)
- **Simulation:** executing the model to observe and analyze behavior

**3. Why simulate?**
- Experiment without risks
- Reduce costs of real tests
- Study scenarios without disturbing the real system
- Make better decisions through prediction

**4. Application domains**
- Industry, transport, health, computing, defense

**5. Types of systems (two independent dimensions)**

| Dimension | Categories |
|---|---|
| Randomness | Deterministic vs. Stochastic |
| Time evolution | Discrete vs. Continuous vs. Hybrid |

**6. Dynamic systems and complexity**
- Systems whose properties change with time
- Complexity challenges: feedback, delays, non-linearities, multivariate aspects, uncertainty

**7. The 6-step iterative modeling process**
1. Problem Definition
2. Conceptual Model Design
3. Mathematical Formalization
4. Numerical Implementation (Coding)
5. Verification & Validation
6. Experimentation & Analysis

**8. Modeling tools**
- Finite State Machines → sequential behavior
- Markov Chains → random systems with memoryless property
- Petri Nets → concurrent/parallel systems
- Queueing Models → arrival/waiting/service systems

**9. Verification vs. Validation**
- Verification: "Did I build the model right?" (code vs. math)
- Validation: "Did I build the right model?" (model vs. reality)
