---
{"dg-publish":true,"permalink":"/regularization/","created":"2026-11-01T16:55:35.153+01:00","updated":"2026-11-01T17:01:46.025+01:00","dg-note-properties":{}}
---

#ml 
***
Regularization is a technique used when your model **overfits** (memorizes the training data too well, including the noise). The solution is to add a **penalty** to the cost function to prevent the weights from becoming too large.

The new cost function is:

![Pasted image ٢٠٢٦١١٠١١٦٥٦٢٧.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A1%D9%A0%D9%A1%D9%A1%D9%A6%D9%A5%D9%A6%D9%A2%D9%A7.png)

- λ is a hyperparameter . 
- If λ=0 there is no regularization (risk of overfitting). 
- If λ is too high, the weights are forced to near zero (underfitting).
    

There are three main types:

1. **Ridge Regression🔫 (L2):** Adds a penalty of the squared weights ![Pasted image ٢٠٢٦١١٠١١٦٥٨١٩.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A1%D9%A0%D9%A1%D9%A1%D9%A6%D9%A5%D9%A8%D9%A1%D9%A9.png). It shrinks weights to be small, but **never exactly zero**. Great for multicollinearity (stabilizing coefficients).
    
2. **Lasso Regression💣️ (L1):** Adds a penalty of the absolute weights ![Pasted image ٢٠٢٦١١٠١١٦٥٨٣٦.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A1%D9%A0%D9%A1%D9%A1%D9%A6%D9%A5%D9%A8%D9%A3%D9%A6.png) This forces some weights to become **exactly zero**, automatically removing useless features (feature selection).
    
3. **Elastic Net💣️🔫:** Combines L1 and L2 (controlled by a parameter ρ). Good for large datasets with correlated variables.
    
