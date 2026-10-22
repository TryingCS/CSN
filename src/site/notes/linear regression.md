---
{"dg-publish":true,"permalink":"/linear-regression/","created":"2026-10-15T23:07:57.225+01:00","updated":"2026-10-22T19:13:36.758+01:00","dg-note-properties":{}}
---

#ml 
Linear regression :
supervised learning algorithm. 🏷️
 goal 🎯: predict a **continuous target variable**.

Think of examples like predicting a house's price,
To do this, the model looks at one or more **explanatory variables** (input features).

"least-squares" method, and later Francis Galton coining the term "regression" .

**Mathematical Formulation:**  
The model assumes a linear relationship between the inputs (X) and the target (Y).

- **Simple Linear Regression** (one input variable):
    

$y_i = w_0 + w_1x_i$


- **Multiple Linear Regression** (multiple input variables):
    
$yi​=w0​+w1​xi1​+⋯+wn​xin​+ϵi​,$  
Where xij is the jj-th feature for the ii-th [[example\|example]], wjwj​ are the weights, and ϵi is the residual error (the difference between the observed and predicted value).  
In vector form:    ![Pasted image ٢٠٢٦١٠٢١٢١١٨١٩.png\|96](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A1%D9%A2%D9%A1%D9%A1%D9%A8%D9%A1%D9%A9.png)
***
## Finding Weights
Two methods :
**1 Analytical Method (The Normal Equation)**
![Pasted image ٢٠٢٦١٠٢٢١٨٤٢١٥.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A2%D9%A1%D9%A8%D9%A4%D9%A2%D9%A1%D9%A5.png)
- **Advantage☀️:** It gives you the exact solution in one step, without any iterations.
- **Limitation📛:** It requires calculating the inverse of a matrix (X^T). If you have a huge number of features (n is very large), this matrix inversion becomes extremely slow and computationally expensive.
**2. Iterative Method (Gradient Descent)**
Instead of solving it all at once, we take small steps downhill to find the minimum of the cost function.
The formula is:
![Pasted image ٢٠٢٦١٠٢٢١٨٤٦٢١.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A2%D9%A1%D9%A8%D9%A4%D9%A6%D9%A2%D9%A1.png)
- **α ([[Learning Rate\|Learning Rate]]):** This controls the size of the step we take.
    
    - If α is too small, convergence is very slow (takes forever).
        
    - If α is too large, the algorithm might overshoot the minimum, diverge, or oscillate around it.
        
- **![Pasted image ٢٠٢٦١٠٢٢١٨٤٧٢٧.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A2%D9%A1%D9%A8%D9%A4%D9%A7%D9%A2%D9%A7.png)(Gradient):** This is the slope. By subtracting it, we move in the direction of the steepest decrease.
    
- **Advantages☀️:** Very efficient for large datasets and high-dimensional models. It doesn't require matrix inversion. It works for any differentiable cost function.
    
	- **Limitations📛:** It gives an approximation, not an exact solution. It's sensitive to data scaling (you often need to [[normalize\|normalize]] your data first).
***
## Numerical Examples

![Pasted image ٢٠٢٦١٠٢٢١٩١١٠٦.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A2%D9%A1%D9%A9%D9%A1%D9%A1%D9%A0%D9%A6.png)
***
![Pasted image ٢٠٢٦١٠٢٢١٩١٣٣٤.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A2%D9%A1%D9%A9%D9%A1%D9%A3%D9%A3%D9%A4.png)