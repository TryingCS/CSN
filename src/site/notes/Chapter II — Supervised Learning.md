---
{"dg-publish":true,"permalink":"/chapter-ii-supervised-learning/","created":"2026-10-15T22:37:31.292+01:00","updated":"2026-11-13T18:12:29.244+01:00","dg-note-properties":{}}
---


#ml 
### **Part 1 — Linear Models and Regularization**
![Pasted image ٢٠٢٦١١٠١١٦٤٢٢٦.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A1%D9%A0%D9%A1%D9%A1%D9%A6%D9%A4%D9%A2%D9%A2%D9%A6.png)


1. [[Supervised learning basics\|Supervised learning basics]]
    
2. [[linear regression\|linear regression]]
    
3. Multiple linear regression
    
4. [[Cost functions\|Cost functions]]
    
5. Training: gradient descent / normal equation
    
6. Polynomial regression
    
7. [[Logistic regression\|Logistic regression]] for classification
    
8. Sigmoid, decision boundary, cross-entropy
    
9. Overfitting vs underfitting
    
10. Regularization: Ridge, Lasso, Elastic Net
***


### The Big Picture

Everything we've done so far falls under **Supervised Learning**: we have inputs (\(X\)) and we have the true answers (\(y\)), and we want to find the weights (\(w\)) that map \(X\) to \(y\). 

Here is the exact connection between the two algorithms:

**1. Linear Regression (Predicting a Number)🧮
*   **The Goal:** Predict a continuous number (e.g., salary).
*   **The Equation:** $ŷ​=w0​+w1​x$
*   **The Output:** Whatever number comes out (e.g., 45,000).
*   **How we train it:** We use **MSE** (Mean Squared Error) and find the weights using either the Analytical method (matrix math) or Gradient Descent.

**2. Logistic Regression (Predicting a Category)** 📦️
*   **The Goal:** Predict a binary category (e.g., Spam vs. Not Spam). We do this by predicting the **probability** (between 0 and 1) of belonging to Class 1.
*   **The Problem:** If we use the linear equation, the output could be any number (like -3.5 or 12), which makes no sense as a probability.
*   **The Solution:** We take that exact same linear equation, and we rename it **\(z\)**.  
*   **The Magic Trick:** We pass \(z\) into the **Sigmoid function**: This forces the output to always be between 0 and 1.
*   **How we train it:** We use **Log Loss** (Cross-Entropy) instead of MSE, but we still find the weights using Gradient Descent. w


Here is the flow:
*   **Linear Regression:** == [Linear Equation] →  
*   **Logistic Regression:** 
* X→ Linear Equation = **\(z\)** → [Sigmoid] → \(\hat{p}\) (Probability)

You don't need to memorize a bunch of disconnected formulas. Just remember: Logistic regression is just Linear Regression with a "squishing" function at the end so we get a probability. 

---
P1

1.  **The Goal:** Find weights (\(w\)) to make accurate predictions.
2.  **Linear Regression:** Predicts numbers. Uses MSE. Trained via Normal Equation (matrix) or Gradient Descent 🏔️(walking down the hill).
3.  **Logistic Regression:** Predicts probabilities/categories. Squishes the linear output (\(z\)) through a Sigmoid function. Uses Log Loss because MSE creates bumpy mountains.
4.  **Regularization:** Stops overfitting by penalizing huge weights. 
    *   *Ridge (L2):* Shrinks weights.
    *   *Lasso (L1):* Deletes features (sets weights to 0).
    *   *Elastic Net:* The combo platter.

---
# Part 2: Decision Trees and Ensemble Methods🌳

Decision trees are a series of "If-Then-Else" questions (like a flowchart).
 learn how the computer decides _which_ questions to ask.
 