---
{"dg-publish":true,"permalink":"/supervised-learning-basics/","created":"2026-10-15T22:39:36.866+01:00","updated":"2026-10-21T14:54:38.137+01:00","dg-note-properties":{}}
---

#ml 

### What is Supervised Learning?

Supervised learning learns from **labeled data**: pairs \((x, y)\).

- \(x\) = input / features  📥️
- \(y\) = target / label / output  📤️
- Goal: learn a function f such that f(x)≈y for new, unseen x.

Two main supervised tasks( based on the nature of the ouput ):

- **[[Regression\|Regression]]**: \(y\) is continuous.  
  Example: predicting house price.
- **Classification**: \(y\) is discrete / categorical.  
  Example: predicting spam / not spam.

- **Binary Classification:** A specific type of classification where Y has exactly two possible values (e.g., spam / not spam, sick / healthy).