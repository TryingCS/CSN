---
{"dg-publish":true,"permalink":"/krr-roadmaps/","created":"2026-10-13T11:01:01.279+01:00","updated":"2026-10-14T18:03:32.581+01:00","dg-note-properties":{}}
---

#krr 


**Course Title:** Knowledge Representation and Reasoning 
**Prerequisites:** Mathematical Logic, Basics of AI.

**What will you learn this semester?**  
The goal: learn how computers can understand the world (Knowledge Representation) and make decisions (Reasoning).

1. **Preliminaries:** Intro to AI & Multi-agent Systems .
    
2. **Classical Logic:** Propositional and Predicate Logic .
    
3. **Non-Classical Logics:** Modal logic, Default logic, Description logic.
    
4. **Uncertainty:** Belief functions, Bayesian networks.
    
5. **Fuzzy Set Theory:** Handling vagueness (e.g., "the weather is hot")♨️.
## from heaviest to lightest:
### 🏆 1. The Heaviest (Volume & Abstraction): 
Chapter 1 (
*Syllabus Section: B- Logique Non classique (Modal, Default, Description)*
This is shaping up to be the **longest chapter in terms of files**. Just look at the sub-topics: it has 3 massive, completely distinct sub-fields (Modal Logic, Default Logic, Description Logic).
*   **Why it's heavy:** Each of these logics introduces entirely new symbols, new rules of inference, and new semantics (like Kripke models for Modal Logic). Description Logic alone is essentially a whole separate language used for building the Semantic Web and ontologies. Expect at least 3️⃣ to 4️⃣ separate PDF "Parts" for this section alone.

### 📐 2. The Heaviest (Mathematically): Chapter 2 - Uncertainty Management
*Syllabus Section: Gestion de l'incertitude (Belief functions, Bayesian Networks)*
*   **Why it's heavy:** This chapter moves away from pure logic (True/False) and dives into **probabilities**. You will need to remember (or relearn) probability theory, conditional probability, and Bayes' Theorem. Bayesian Networks require understanding complex graph theory (Directed Acyclic Graphs), joint probability distributions, and conditional independence. It is mathematically dense and can be very tricky if your probability foundations aren't solid.

### 🍰 3. The Lightest (Most Intuitive): Chapter 3 - Fuzzy Set Theory
*Syllabus Section: La theorie des sous-ensembles flous*
*   **Why it's light:** Compared to the strict binary logic of Chapter 1 and the heavy math of Chapter 2, Fuzzy Logic is very intuitive. Instead of everything being strictly True (1) or False (0), things can be "mostly true" (e.g., 0.8). It deals with degrees of truth. The concepts of fuzzy controllers (like a thermostat that adjusts gradually) are highly practical, visual, and easier to grasp conceptually. 

---

### 📊 Summary Table:

| Chapter                | Length    | Math Difficulty         | Conceptual Difficulty | Total Weight   |
| :--------------------- | :-------- | :---------------------- | :-------------------- | :------------- |
| **Ch 1 (Part B)**      | 🔴 High   | 🟡 Medium               | 🔴 High (Abstract)    | **Very Heavy** |
| **Ch 2 (Uncertainty)** | 🟡 Medium | 🔴 High (Probabilities) | 🟠 Medium-High        | **Heavy**      |
| **Ch 3 (Fuzzy)**       | 🟢 Low    | 🟢 Low                  | 🟢 Low (Intuitive)    | **Light**      |

### 🧠 Strategic Advice:
1.  **For Chapter 1 (Part B):** Don't memorize the symbols blindly. Focus on the *meaning* and *application*. For example, in Modal Logic, understand *why* we need to represent "belief" or "necessity." 
2.  **For Chapter 2 (Uncertainty):** **Review your probability basics NOW.** Before the teacher uploads the file, make sure you know what [[Conditional probability\|Conditional probability]] `P(A|B)` is, and understand [[Bayes’ Theorem\|Bayes’ Theorem]]. If you are solid on the math, Chapter 2 becomes much easier.
3.  **For Chapter 3 (Fuzzy):** it's highly practical and less abstract than the rest.
***
### ch1 




If we look at your syllabus (Syllabus.pdf), Chapter 1 is titled **"Logiques non classiques"** (Non-Classical Logics). It is divided into two main sections:
*   **A- Logique Classique** (Classical Logic) ← **YOU ARE HERE** (This is your "Part 1" PDF).
*   **B- Logique Non classique** (Non-Classical Logic) ← Still to come.
A:
1.  Propositional Logic (Syntax, Semantics, Truth Tables)
2.  Normal Forms (FNC, FND)
3.  Predicate Logic (Quantifiers, Free/Bound variables, Prenex and Skolem Normal Forms).

 The rest of the chapter (Part B) gets more philosophical and deals with how to model complex ideas like beliefs, exceptions, and structured knowledge.

### 📂 Question 2: How many "parts" files should I expect?

The teacher named this file "Part 1", which strongly implies there will be a "Part 2". However, based on the syllabus, **you should expect multiple parts for the rest of Chapter 1**, because Section B is massive. 

Here is my prediction for how the teacher will upload the remaining files for Chapter 1 (Section B):
*   **Part 2: Logique Modale** (Modal Logic). This will cover notions of "necessary" and "possible" truths, Kripke semantics (possible worlds), and how multi-agent systems communicate.
*   **Part 3: La logique des défauts** (Default Logic). This covers "non-monotonic" reasoning—how to draw conclusions when you don't have all the information (e.g., "Birds normally fly, so if I see a bird, I assume it flies, unless I know it's a penguin").
*   **Part 4: Logiques de description** (Description Logics). This is heavily used for building ontologies (structured knowledge bases) and the semantic web. 

**What about the rest of the semester?**
Looking at your syllabus, you have two more major chapters after Chapter 1:
*   **Chapter 2 (Uncertainty):** Belief functions, Bayesian networks. Expect this to be split into **2 to 3 parts**.
*   **Chapter 3 (Fuzzy Set Theory):** Handling vagueness (e.g., "the weather is hot"). Expect this to be **1 to 2 parts**.

**Total Estimate:** You can probably expect **6 to 10 more PDF files** across the entire semester. 

🧠 What should you do right now?

**Do not wait for the next files to arrive.** The concepts in Part 1 are the alphabet of the entire course. If you don't understand how `p ⇒ q` works, you will struggle with Modal Logic (which adds new symbols to it). 

Here is your action plan for this week:
1.  **Master the Truth Tables:** Write down the truth table for `AND`, `OR`, `IF...THEN` (`⇒`), and `IF AND ONLY IF` (`⇔`). Memorize the `⇒` rule (it's only false when True implies False).
2.  **Practice FNC Conversion:** Take a random formula like `¬(p ∧ q) ⇒ (r ∨ s)` and try to convert it to Conjunctive Normal Form using the algorithm in the PDF.
3.  **Understand Quantifiers:** Make sure you can explain the difference between `∀x (Human(x) ⇒ Mortal(x))` and `∃x (Human(x) ∧ Mortal(x))`. 
4.  **Try the Vacuum Cleaner PEAS:** Draw the vacuum cleaner environment and write out its PEAS (Performance, Environment, Actuators, Sensors).

