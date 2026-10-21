---
{"dg-publish":true,"permalink":"/cost-functions/","created":"2026-10-21T21:28:35.947+01:00","updated":"2026-10-21T21:38:37.434+01:00","dg-note-properties":{}}
---

#ml
---

Now that we know what the model is, how do we find the best weights (\(w\))? We need a way to measure how wrong our predictions are. This is the **Cost Function** (or Loss Function). 

The most common one for linear regression is the:
## **Mean Squared Error (MSE)**:
![Pasted image ٢٠٢٦١٠٢١٢١٣٠٤٧.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A1%D9%A2%D9%A1%D9%A3%D9%A0%D9%A4%D9%A7.png)
- m = the total number of examples (rows).
    
- yi= the actual value.
    
- ŷ​i​ = our model's predicted value.
    
- The 1/2​ is just a mathematical trick to make the derivative cleaner later when we use Gradient Descent.



If our model perfectly predicts the target value for every single example in the training set, what would the Mean Squared Error (MSE) be?
***

