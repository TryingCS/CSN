---
{"dg-publish":true,"permalink":"/stacking-and-blending/","created":"2026-11-14T20:09:29.375+01:00","updated":"2026-11-14T20:15:40.685+01:00","dg-note-properties":{}}
---

#ml 
***
We've covered homogeneous ensembles (where all models are trees). Now let's look at the third family: **Heterogeneous Ensembles**, where we mix fundamentally different models together.

### Stacking and Blending🎨

#### The Core Idea 
Bagging and Boosting combine multiple versions of the *same* algorithm (usually trees). 
**Stacking** takes a different approach: it combines completely different algorithms (e.g., a Linear Regression, a Random Forest, an SVM, and a Neural Network). 

The idea is: *No single algorithm is optimal for every type of data.* A linear model might capture the general trend, while a tree might capture the non-linear interactions. So, why not combine them?

#### The Architecture: Level 0 and Level 1
Stacking is a multi-level architecture:
*   **Level 0 (Base Learners):** You train several different models on your original data $X$. They each produce a prediction $\hat{y}_1, \hat{y}_2, \dots$.
*   **Level 1 (Meta-Learner):** You train a new model. But this model does **not** look at the original features \(X\). Instead, it looks at the predictions from Level 0 as its new features. It learns *how to combine* the base models' predictions. 

The meta-learner's job is to figure out: *"When the Linear Regression says X, and the Tree says Y, who should I trust more?"*

#### The Trap: Data Leakage 🪣💦
If you train the Base Models on the training set, and then use those *same* predictions to train the Meta-Model, you will fail. 
*   **Why?** Because the Base Models have memorized the training data (overfitting). Their predictions on that data are "too perfect." The Meta-Model will learn to trust these perfect predictions, but when you give it new test data, the Base Models will make normal errors, and the Meta-Model won't know how to handle them. This is called **Data Leakage**.

#### The Solution: K-Fold Stacking (Out-of-Fold)
To fix Data Leakage, we use **K-Fold Cross-Validation** to generate the meta-features:
1.  Split your training data into \(K\) folds (e.g., 5).
2.  Train the Base Models on 4 folds, and predict on the 5th fold (the one they haven't seen). These are the **Out-Of-Fold (OOF)** predictions.
3.  Repeat this \(K\) times so every data point gets an honest, unbiased prediction.
4.  Use these OOF predictions to train the Meta-Model. 

#### The Simpler Alternative: Blending
K-Fold Stacking is highly robust, but it requires training the Base Models \(K\) times, which is computationally expensive. 

**Blending** is the faster, simpler alternative:
1.  Instead of K-Folds, just split your data once into a Training set (80%) and a Validation set (20%).
2.  Train the Base Models on the Training set.
3.  Predict on the Validation set.
4.  Train the Meta-Model on those predictions.
5.  (For the final test, you re-train the base models on the full 100% training data).

 Blending is faster and easier to implement, but it wastes data 
 Stacking is slower but maximizes data efficiency and robustness.

***
