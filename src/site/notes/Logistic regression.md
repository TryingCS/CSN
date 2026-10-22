---
{"dg-publish":true,"permalink":"/logistic-regression/","created":"2026-10-22T19:14:38.836+01:00","updated":"2026-10-22T19:24:59.276+01:00","dg-note-properties":{}}
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