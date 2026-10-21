---
{"dg-publish":true,"permalink":"/simple-linear-regression/","created":"2026-10-15T23:07:57.225+01:00","updated":"2026-10-21T21:22:26.383+01:00","dg-note-properties":{}}
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
