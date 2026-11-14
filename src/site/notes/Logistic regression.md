---
{"dg-publish":true,"permalink":"/logistic-regression/","created":"2026-10-22T19:14:38.836+01:00","updated":"2026-11-01T16:55:35.272+01:00","dg-note-properties":{}}
---

#ml 
***

[[linear regression\|Linear regression]] predicts continuous values, but what if we want to predict categories?

(likelyhood of belonging to a category)

**Logistic Regression** solves this. It keeps the linear part: $z=w^TX+w0$​. 
But it passes z through a**Sigmoid function**:
						![Pasted image ٢٠٢٦١٠٢٢١٩١٨٠٣.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A2%D9%A1%D9%A9%D9%A1%D9%A8%D9%A0%D9%A3.png)
This  function "squeezes" any number (from −∞ to +∞) into a probability between **0 and 1**.

- If z=0, p^=0.5.
    
- If z is very large positive, p^≈1.
    
- If z is very large negative, p^≈0.
    

**Decision Rule:** If p^≥0.5 we classify as Class 1. Otherwise, Class 0.
***
###  Limitations of Logistic Regression

Even though logistic regression is the baseline for classification📦️ it has weaknesses:

1. **Linearity assumption:** It assumes the relationship between the variables and the _log-odds_ (the zz part) is linear. If the real-world relationship is highly complex and curved, the model's predictions will be biased.
    
2. **Poor on non-linearly separable data:** If the classes heavily overlap (imagine red and blue dots mixed in a circle), a straight line can't separate them well.
    
3. **Sensitive to correlated variables (Multicollinearity):** If two variables are highly correlated (e.g., "years of experience" and "age"), the model's weights become unstable and hard to interpret.
    
4. **Doesn't handle complex interactions directly:** It struggles to capture the combined effect of two variables (like X1×X2​) unless you manually create that feature.
## Examples for limits
### : Multicollinearity (Unstable Weights)

Imagine we are predicting if a patient is **Sick (1)** or **Healthy (0)** using two features:

- x1=Weight (in kg)
    
- x2= Height (in cm)
    

Weight and Height are highly correlated (taller people tend to weigh more). Let's say the true underlying relationship is simply that heavier people are slightly more likely to be sick.

- If we used **only** Weight: The model might learn 
              z=−50+0.4(x1)
    
- If we used **only** Height: The model might learn 
			  z=−50+0.3(x2)
    

**The Multicollinearity Issue:** When we put _both_ into the model, z=w0+w1x1+w2x2z=w0​+w1​x1​+w2​x2​, the model gets confused. Because x1 and x2 move together, the model can achieve the exact same accuracy with completely different weights. It might learn:

z=−50+500(x1)−499(x2)z=−50+500(x1​)−499(x2​)

_Why is this bad?_ The weights (500500 and −499−499) are massive and have opposite signs. The model is mathematically "canceling out" Height. If you get a new patient who is 1cm taller, the model's prediction will swing wildly. It makes the model **unstable** and impossible to interpret (you can't say "Weight increases sickness risk" because the weight is artificially huge).

###  Non-linearly Separable Data (Overlap)

Imagine a 1D dataset where we are trying to classify the class using just one feature xx:

- x=1→y=0 (Class 0)
    
- x=2→y=1 (Class 1)
    
- x=3→y=0 (Class 0)
    

Look at the pattern: the classes alternate! (0, 1, 0). A straight line (linear boundary) cannot separate this.  
Let's try to do the math: Our model is z=w0+w1x. Remember, if z≥0, we predict Class 1.

- For x=2 (Class 1), we need w0+2w1≥0
    
- For x=1x=1 (Class 0), we need w0+w1<0
    
- For x=3x=3 (Class 0), we need w0+3w1<0
    

**Contradiction!** w1​ cannot be both positive and negative. The math proves it is **impossible** for a logistic regression model to separate this data. No matter what weights you choose, it will always make an error on at least one point. The model will just keep oscillating and never converge perfectly.

---

the solution :  [[Regularization\|Regularization]]