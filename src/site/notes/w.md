---
{"dg-publish":true,"permalink":"/w/","created":"2026-10-21T21:34:41.198+01:00","updated":"2026-10-22T18:57:48.426+01:00","dg-note-properties":{}}
---

#ml 

**The whole goal of "training" the model is simply to find the exact values of these weights (w) that make the predictions as accurate as possible.**
***
Think of **weights** (often called **coefficients** or **parameters**) as the **"importance scores"** or **"multipliers"** that the model learns.

If xij​ is the data you _give_ the model (the inputs), 
the weights wj are ==what the model _figures out_ during training==. They tell you **how much each feature influences the final prediction**.

Let's use the **salary prediction example** 

ŷ=40000+2500x

- **w0=40000: This is the **bias** (or intercept). It's the baseline prediction if all features are zero. (e.g., A person with 0 years of experience still gets a base salary of 40,000).
    
- **w1=2500: This is the **weight** for the feature "years of experience." It tells us the _relationship_: for every 1 additional year of experience (x), the salary increases by 2,500.
    

Going back to the geometric view 

- **w1​** is the **slope** of the line (how steep it is).
    
- **w0​** is the **intercept** (where the line crosses the y-axis).
    

In a multiple linear regression, if you have 5 features (e.g., square footage, number of rooms, age of house, etc.), you will have 5 weights (plus the bias w0​). If the weight for "number of rooms" is very high, it means that feature has a huge impact on the price. If a weight is near zero, it means that feature doesn't matter much.
***
**The objective of learning:** We want to find the parameter vector \([[w\|w]]\) that *minimizes* this error \(J(w)\). Geometrically, this means finding the straight line (or hyperplane) that passes as closely as possible to all the data points. 
***
## Finding weights

**The Analytical Method (Normal Equation):** This specific matrix formula is **specific to Linear Regression** (and specifically when using the MSE cost function). It's a shortcut that works _only_ because the MSE cost function for linear regression is shaped like a perfect bowl (convex), and we can mathematically find the exact bottom of that bowl in one step.
***
- **The Iterative Method (Gradient Descent):** This is a **general optimization technique**. Gradient Descent is a universal tool used across almost all of ML. 