---
{"dg-publish":true,"permalink":"/simple-linear-regression/","created":"2026-10-15T23:07:57.225+01:00","updated":"2026-10-15T23:10:17.558+01:00","dg-note-properties":{}}
---

#ml 
Linear regression is our first supervised learning algorithm. Its goal is to predict a **continuous target variable**.

Think of examples like predicting a house's price, a student's test score, or a company's revenue. To do this, the model looks at one or more **explanatory variables** (input features).

the method dates back to 1805 🦴 with Legendre and Gauss formalizing the "least-squares" method, and later Francis Galton coining the term "regression" in 1886.

**Mathematical Formulation:**  
The model assumes a linear relationship between the inputs (X) and the target (Y).

- **Simple Linear Regression** (one input variable):
    

y_i = w_0 + w_1x_i  
]  
Here, w0w0​ is the intercept, and w1w1​ is the slope.

- **Multiple Linear Regression** (multiple input variables):
    
yi​=w0​+w1​xi1​+⋯+wn​xin​+ϵi​,  
Where xijxij​ is the jj-th feature for the ii-th example, wjwj​ are the weights, and ϵiϵi​ is the residual error (the difference between the observed and predicted value).  
In vector form, this is neatly written as: y^=Xwy^​=Xw

**Quick Check (MCQ):**  
In the multiple linear regression formula yi=w0+w1xi1+⋯+wnxin+ϵiyi​=w0​+w1​xi1​+⋯+wn​xin​+ϵi​, what does the term ϵiϵi​ represent?

A) The predicted value for the ii-th example  
B) The weight of the ii-th feature  
C) The residual error for the ii-th example  
D) The intercept of the line