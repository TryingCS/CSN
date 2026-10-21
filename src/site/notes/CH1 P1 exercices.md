---
{"dg-publish":true,"permalink":"/ch-1-p1-exercices/","created":"2026-10-21T14:34:39.924+01:00","updated":"2026-10-21T15:10:49.370+01:00","dg-note-properties":{}}
---

#ml 
Good plan. Let's start gentle but meaningful. I'll break this into rounds. This first round covers the very basics — what ML is, how it differs from traditional programming, and the core vocabulary. No history dates, no Python, no coefficients.

When you're done, tell me how it felt (too easy, just right, too hard) and we'll adjust.

---

## Round 1: Baby Steps — What is ML?

**Q1.** In one or two sentences, what is the key difference between traditional programming and machine learning?

**Q2.** True or False: In machine learning, the programmer explicitly writes the rules that the system uses to make decisions.

**Q3.** Fill in the blank:

In traditional programming, you provide **data** and **\_\_\_\_\_\_\_\_** to the computer, and it produces a **result**.

In machine learning, you provide **sample data** and **\_\_\_\_\_\_\_\_** to the computer, and it produces a **\_\_\_\_\_\_\_\_**.

**Q4.** What is a **model** in machine learning? Choose the best answer:

A) A set of hand-written if-then rules  
B) The learned mapping from inputs to outputs, produced by training on data  
C) The dataset used during training  
D) The computer program that collects data

**Q5.** Which of the following best describes **generalization**?

A) The model memorizes the training data perfectly  
B) The model performs well on new, unseen data  
C) The model runs quickly on large datasets  
D) The model uses more data to improve

**Q6.** Why is generalization important in machine learning? Answer in one sentence.

**Q7.** Match each term to its correct description:

| Term | Description |
|------|-------------|
| 1. Features | a. The expected output for a training example |
| 2. Label | b. The input information used to make a prediction |
| 3. Training | c. Using the model on new data |
| 4. Prediction | d. The process of learning the model from data |

**Q8.** True or False: A model that performs perfectly on training data but poorly on new data has generalised well.

**Q9.** In the ML project workflow, what is the correct order of these steps?

- Training
- Collect data
- Evaluation
- Preprocess
- Improvement
- Choose the algorithm

**Q10.** What does the "Training" step actually do? Choose the best answer:

A) Collects raw data from the internet  
B) Adjusts the model's parameters so it better maps inputs to outputs  
C) Tests the model on unseen data  
D) Cleans and encodes the data

**Q11.** Why do we evaluate a model on **unseen** data rather than the data it was trained on?

**Q12.** True or False: The more numerous and representative the training data, the more effectively the algorithm can learn.

---

### Answers and brief explanations

**A1.** Traditional programming: humans write the rules; the computer applies them. ML: the computer learns the rules (the model) from data, without being explicitly programmed for each specific task.

**A2.** False. The whole point of ML is that the rules are learned from data, not hand-written.

**A3.** Traditional: data + **handcrafted model** → result.  
ML: sample data + **expected result** → **model**.

**A4.** B. A model is the learned mapping from inputs to outputs. It's produced by training, not hand-written.

**A5.** B. Generalization = performing well on new, unseen data.

**A6.** Because the goal is to make correct predictions on data the model has never seen before — not just to memorize the training set. A model that only memorises is useless in practice.

**A7.** 1–b, 2–a, 3–d, 4–c.

**A8.** False. That's the opposite — it has overfit (memorised) and failed to generalise.

**A9.** Collect data → Preprocess → Choose the algorithm → Training → Evaluation → Improvement.

**A10.** B. Training adjusts the model's parameters to reduce error on the training data.

**A11.** Because if you test on training data, you're measuring memorisation, not generalisation. Unseen data tells you whether the model actually learned patterns that transfer.

**A12.** True. More numerous and representative data generally leads to better learning — this is one of the essential characteristics of ML (slides 10–11).


---

##  Round 2?

learning types now. . We’ll start with the two most fundamental ones: **Supervised vs. Unsupervised**.



**Q1.** What is the defining characteristic of **supervised learning**? What does the training data look like?
Labeled 
**Q2.** Give one example of a supervised learning task that is a **regression** problem, and one that is a **classification** problem.
regression:  predicting house prices
classification: is the object in the photo pizza or not pizza
**Q3.** What is the defining characteristic of **unsupervised learning**? What does the training data look like?
No predefined categories/labels
**Q4.** True or False: In unsupervised learning, the algorithm discovers the "correct" labels for the data.
true
**Q5.** Match the task to the learning type (Supervised or Unsupervised):

A) Grouping customers into segments based on buying habits.  
B) Predicting whether a bank transaction is fraudulent. supervised? cause we have two predefined labels ?
C) Reducing a dataset of 100 features down to 3 main components. 
D) Predicting the price of a house based on its size and location.  supervised? 

**Q6.** If you have a dataset with 1,000 rows of data, and *none* of the rows have a target/output column, what type of learning are you limited to?
unsupervised 
**Q7.** Which of these is a typical algorithm for **unsupervised** learning?
A) Linear Regression
B) Logistic Regression
C) K-Means =
D) SVM

**Q8.** Which of these is a typical algorithm for **supervised** learning?
A) PCA
B) DBSCAN
C) t-SNE
D) Decision Trees =

**Q9.** Why might you choose unsupervised learning over supervised learning? (Think about the data you have available).
too expensive to label , the goal is to just recoginze patterns not find a label for each entry
**Q10.** In one sentence, what is the goal of unsupervised learning? (Hint: it's not predicting a label). 
clustering , discovering patterns 
### No big oof at all! You actually did really well. You got 8 out of 10 perfectly right (or basically right). There is only **one major conceptual trap** you fell into, which is very common. Let's check them.

- **Q1:** Correct, but a bit brief. For an exam, you'd say: "The model learns from **labeled data** (input features + the expected output/target)."
- **Q2:** Perfect. House prices = continuous number (regression). Pizza or not pizza = category (classification).
- **Q3:** Correct. The training data has features but **no target column**.
- **Q4:** ❌ **False (This is the trap!)**
  - *Why?* The algorithm does **not** discover the "correct" labels. It discovers **groups/clusters**, but it doesn't know what they mean. 
  - *Example:* If you feed customer data to K-Means, it might group them into Cluster A and Cluster B. It doesn't know that Cluster A is "young spenders" and Cluster B is "older savers". **A human** has to look at the clusters afterward and assign meaning to them. Unsupervised learning finds *structure*, not *correct answers*.
- **Q5:** 
  - A) Unsupervised (Clustering).
  - B) Supervised. Your reasoning ("cause we have two predefined labels") is **exactly** right. 
  - C) Unsupervised (Dimensionality reduction).
  - D) Supervised. Correct.
- **Q6:** Correct. Unsupervised.
- **Q7:** Correct, K-Means.
- **Q8:** Correct, Decision Trees.
- **Q9:** **Excellent answer.** "Too expensive to label" is the #1 reason people use unsupervised learning. 
- **Q10:** Correct. Clustering and discovering hidden patterns/structures.

---

### Why Q4 is such a common trap
People often think unsupervised learning is "finding the labels the data already has." It's not. It's like being given a box of mixed LEGO bricks and sorting them by color and shape. You made the piles (clusters), but no one told you what they are called. You discovered the *structure*.

---

You are doing great. You clearly understand the difference between supervised (predicting a known answer) and unsupervised (finding structure without answers). 

Do you want to do **Round 3** (Semi-supervised, Reinforcement, and Self-supervised)? Or do you want to pause, review these, and come back? Round 3 will be a bit quicker since we already talked through the concepts.