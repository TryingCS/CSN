---
{"dg-publish":true,"permalink":"/normalize/","created":"2026-10-22T19:09:40.540+01:00","updated":"2026-10-22T19:10:09.021+01:00","dg-note-properties":{}}
---

#ml 
### What does "Normalizing Data" mean?

Imagine you are predicting house prices using two features:

1. Number of bedrooms (ranges from 1 to 5).
    
2. Square footage (ranges from 1,000 to 10,000).
    

Because square footage has much larger numbers, the cost function becomes stretched out like a very long, narrow, steep canyon rather than a nice round bowl. Gradient descent will bounce violently between the steep walls of the canyon instead of going straight down to the bottom.

**Normalization** means scaling all your features so they fall into a similar range (e.g., forcing them all to be between 0 and 1). This turns the canyon back into a smooth bowl, allowing Gradient Descent to converge much faster.