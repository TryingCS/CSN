---
{"dg-publish":true,"permalink":"/ml-ch-2-p1-qa/","created":"2026-11-01T17:29:02.180+01:00","updated":"2026-11-01T20:24:53.590+01:00","dg-note-properties":{}}
---



#ml regression is about predicting the **exact quantity**, while logistic regression is about predicting the **likelihood of a category**.

---

**1. Regression vs. Classification**
*   Regression is when \(Y\) is **continuous** (predicting a number like salary/price). Classification is when \(Y\) is **discrete** (predicting a category). 
* *Note: Regression predicts a number, not a probability. Logistic Regression (which is a classification algorithm) is the one that predicts a probability.*

**2. \(w_1\) geometrically**
* It's the slope of the line.

**3. Why use MSE?**
*   *Your answer:* "to properly handle big weights that just happen to be negative?"
*   *Correction:* Close, but it's about the **errors**, not the weights. If we just added up the errors \((y - \hat{y})\), a positive error (+5) and a negative error (-5) would cancel each other out to 0, making the model think it's perfect! By **squaring** the errors, we make sure all errors are positive, so they add up correctly.

**4. Learning rate**

*   the step size the algorithm takes down the hill.

**5. Large learning rate**
*   *Your answer:* "oscillates and never converges or something like that"
*   *Verdict:* **Perfect!** It bounces back and forth over the minimum and can even diverge (go up the mountain).

**6. Why not linear for probabilities?**
*   *Your answer:* "linear regression gives any number, which wouldn't make sense on its own for a probability"
*   *Verdict:* **Perfect!** You nailed the exact reason. A probability must be between 0 and 1, but a linear line goes from \(-\infty\) to \(+\infty\).

**7. Sigmoid at \(z = 0\)**

*   *Answer:* The formula is ![Pasted image ٢٠٢٦١١٠١١٧٣٣٥٥.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A1%D9%A0%D9%A1%D9%A1%D9%A7%D9%A3%D9%A3%D9%A5%D9%A5.png) 
* If \(z = 0\)  (Exactly 50% probability).

**8. Why Log Loss instead of MSE?**
*   *Answer:* Because MSE creates a "bumpy" (non-convex) cost function when combined with the sigmoid. Gradient descent might get stuck in a local minimum (a small dip) and never find the true bottom. Log Loss is always a smooth bowl (convex).

**9. Multicollinearity**
* two features are highly correlated, which makes the weights unstable.

**10. Which regularization deletes features?**

*   1 (Lasso) sets useless weights to exactly zero.

---
## calc is short for calculator 


### Answering your question: "Regression predicts a number, not a probability"
You asked: *"so it just predicts a feature Y with no meta meaning behind it or what?"*

Actually, it **does** have a meta meaning—the meaning is just tied directly to the **units of your target variable**. 
*   If you use Linear Regression to predict a house price, the output \(\hat{y}\) is literally in dollars (e.g., 250,000). It is saying: *"My best estimate for the price of this house is exactly 250,000."*
*   It is **not** saying: *"There is a 75% chance the house is worth 250,000."* 

In contrast, **Logistic Regression (Classification)** gives a *probability*. It says: *"There is an 85% chance this email is Spam."* 

So, regression is about predicting the **exact quantity**, while logistic regression is about predicting the **likelihood of a category**.

---

### 🧮 Your Quick Numerical Exercises

Grab a piece of paper and a calculator (or just use your head!). Here are two quick exercises based on the exact formulas in your slides. 

#### Exercise 1: Linear Regression (MSE & Gradient Descent)
We have a tiny dataset of 2 examples:
*   \(x_1 = 1\), \(y_1 = 4\)
*   \(x_2 = 2\), \(y_2 = 7\)

We initialize our model with random weights: **\(w_0 = 0\)** and **\(w_1 = 2\)**. 
Our learning rate is **\(\alpha = 0.1\)**.

**Questions:**
1.  **Predictions:** What are our predicted values \(\hat{y}_1\) and \(\hat{y}_2\)? (Use \(\hat{y} = w_0 + w_1x\))
2.  **MSE:** Calculate the Mean Squared Error using the slide formula: \(J(w) = \frac{1}{2m}\sum(y_i - \hat{y}_i)^2\). *(Hint: \(m=2\), so you divide by 4).*
3.  **Gradient Descent Step:** Let's update \(w_1\). The formula from the slides is:
    \(w_1 = w_1 - \alpha \frac{1}{m} \sum (\hat{y}_i - y_i)x_i\)
    Plug in your numbers and find the new \(w_1\).

#### Exercise 2: Logistic Regression (Sigmoid)
Suppose we trained a logistic regression model to predict if a student passes (1) or fails (0) based on study hours. The model learned the linear equation: **\(z = -3 + 1.5x\)**.

**Questions:**
1.  **Calculate \(z\):** A student studies for **\(x = 2\)** hours. What is \(z\)?
2.  **Calculate Probability:** Use the sigmoid formula \(\hat{p} = \frac{1}{1 + e^{-z}}\). 
    *(Don't panic about the math! If \(z = 0\), \(\hat{p} = 0.5\). If \(z = 1\), \(e^{-1} \approx 0.37\), so \(\hat{p} \approx 0.73\). You can just approximate it!)*
3.  **Decision:** Based on the decision rule (if \(\hat{p} \geq 0.5\), predict Class 1), does the model predict this student will pass or fail?

Take your time! Show me your step-by-step answers (even if they are messy or wrong), and we'll review them together.