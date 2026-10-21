---
{"dg-publish":true,"permalink":"/example/","created":"2026-10-21T21:22:35.304+01:00","updated":"2026-10-21T21:26:47.374+01:00","dg-note-properties":{}}
---

#ml 
Example =  an _instance_, _data point_, _observation_, or _row_
== **one single labeled item in the dataset**.

Here is how to visualize it:  
Imagine your dataset is a table (like an Excel sheet):

- **The whole dataset** is the entire table (all the rows).
    
- **An example (i)** is **one single row** in that table. If you have 100 houses in your dataset, you have 100 examples (from i=1i=1 to i=100i=100).
    
- **A feature (j)** is a **column** in that table (like square footage, number of rooms, etc.).
***
So, if we look at the formula for **Example 2** (the second row, i=2) where we want to predict the price of a house based on its size (xi1) and number of rooms (xi2):
![Pasted image ٢٠٢٦١٠٢١٢١٢٥٤٨.png](/img/user/Pasted%20image%20%D9%A2%D9%A0%D9%A2%D9%A6%D9%A1%D9%A0%D9%A2%D9%A1%D9%A2%D9%A1%D9%A2%D9%A5%D9%A4%D9%A8.png)
- y2​ is the actual price of the _second_ house.
    
- x21​ is the size of the _second_ house (the 1st feature of the 2nd example).
    
- x22​ is the number of rooms of the _second_ house (the 2nd feature of the 2nd example).
    
- ϵ2​ is the error for the _second_ house.
    

So, xij simply means: _"Look at row i(the example), and look at column j (the feature)."_