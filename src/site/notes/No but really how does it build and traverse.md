---
{"dg-publish":true,"permalink":"/no-but-really-how-does-it-build-and-traverse/","created":"2026-11-13T18:37:51.093+01:00","updated":"2026-11-13T18:44:37.817+01:00","dg-note-properties":{}}
---

#ml 
***
if the model is just a static data structure, how does it create the rules?

Let's clear this up by separating the **algorithm** (the builder) from the **model** (the finished product).

### 1. Does it create a new tree for each candidate split?
**No.** It does not build a whole tree for every candidate question. That would be incredibly slow. 

Instead, it builds the tree **incrementally, node by node**. 🏠️

Here is the actual step-by-step process (which we'll see mathematically in the slides soon):

1.  **Start at the root** with all your data.
2.  **Test Candidate 1** (e.g., "Age < 30"): The algorithm temporarily splits the data into two buckets🪣. It calculates the "impurity" of those two buckets.
3.  **Test Candidate 2** (e.g., "Income > 50k"): It temporarily splits the data again. Calculates impurity.
4.  **Pick the Winner**: It finds the best split (the one that made the buckets purest).
5.  **Update the Data Structure**: *Now*, and only now, does it write this best split into the tree data structure (those arrays we talked about). It creates a new "node" in the arrays.
6.  **Move Down**: It takes the data from the left bucket, and repeats the whole process to find the best split for that specific bucket.

So, the tree structure is **dynamic**. It starts as just a single root node, and the algorithm keeps adding nodes to the arrays as it finds good splits.

### 2. Who creates the rules, and who performs the traversal?
You have two distinct phases in machine learning, and it's easy to blend them together:

*   **Phase 1: Training (The Algorithm builds the rules)**
    *   You give data to the algorithm (like `fit()` in Python). 
    *   The algorithm does all the "thinking" (testing splits, calculating impurity). 
    *   Its only job is to fill out those arrays (the data structure) with the best questions and thresholds.
    *   Once training is done, **the algorithm is thrown away**. It has done its job.

*   **Phase 2: Prediction (The Model runs the traversal)**
    *   The "Model" is just the saved data structure (the arrays). It doesn't "think" anymore. 
    *   When you call `predict()`, a very simple function just starts at the root node and follows the pointers based on the `if/else` logic stored in the arrays. 
    *   The model itself isn't actively creating rules during prediction; it's just reading the map that the training algorithm drew.

### A concrete example:
Look at the CART example with the **Study Hours**. 
*   The algorithm didn't build 5 different trees for thresholds 2.5, 3.5, 4.5, 5.5, and 7. 
*   It just temporarily split the *data* for each threshold, calculated the Gini score, saw that **4.5** gave a Gini of 0 (perfectly pure), and wrote *that one split* into the tree structure. 
*   That's why it says "The algorithm selects \(t^* = 4.5\)". It didn't build a forest of trees to find it; it just did the math on the fly.

***

**Summary:**
The **Algorithm** is the builder that creates the rules and assembles the data structure during training. The **Model** is just the resulting data structure, which is later used to perform the simple traversal during prediction. 

