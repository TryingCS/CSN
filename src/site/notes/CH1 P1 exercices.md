---
{"dg-publish":true,"permalink":"/ch-1-p1-exercices/","created":"2026-10-21T14:34:39.924+01:00","updated":"2026-10-21T20:55:00.123+01:00","dg-note-properties":{}}
---

#ml 
Good plan. Let's start gentle but meaningful. I'll break this into rounds. This first round covers the very basics — what ML is, how it differs from traditional programming, and the core vocabulary. No history dates, no Python, no coefficients.

When you're done, tell me how it felt (too easy, just right, too hard) and we'll adjust.

---

## Round 1: What is ML?

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
### Solutions

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

***

## Round 3 : Remaining learning types
**Q1.** What is the defining characteristic of **semi-supervised learning**? What does the dataset look like?

**Q2.** Why would a company choose semi-supervised learning instead of purely supervised learning?

**Q3.** Reinforcement Learning (RL) is famous for not having a static dataset. Instead, it has an **agent** interacting with an **environment**. 
What are the two things the agent receives after it takes an action? (Hint: one is a new state, what is the other?)

**Q4.** True or False: In Reinforcement Learning, the agent is given a labeled dataset of "correct actions" so it knows exactly what to do at every step.

**Q5.** What is the ultimate goal of a Reinforcement Learning agent? Choose the best answer:
A) To group similar states together
B) To predict the next state perfectly
C) To learn an optimal policy that maximizes cumulative reward over time
D) To create fake labels from the environment

**Q6.** In **self-supervised learning**, the model learns from raw data without any human labels. How does it get the "answers" it needs to learn?

**Q7.** Which of the following is a classic example of a self-supervised pretext task?
A) Sorting customers into 3 groups
B) Hiding 15% of the words in a sentence and training the model to predict them
C) Training a robot to walk using a reward system
D) Using 100 labeled emails and 10,000 unlabeled emails to detect spam

**Q8.** What is the main difference between **self-supervised** and **semi-supervised** learning? (Hint: think about the role of human labels).

**Q9.** Match the scenario to the correct learning type (Supervised, Unsupervised, Semi-supervised, Reinforcement, Self-supervised):

A) A model is trained on 500 labeled medical images and 50,000 unlabeled medical images.
B) A model is given 1 million raw sentences and learns by predicting the next word.
C) A robot learns to navigate a maze by getting +10 points for reaching the end and -5 points for hitting a wall.
D) A model is given a dataset of images with tags (e.g., "cat", "dog") and learns to classify them.
E) A model is given a dataset of customer purchases with no tags and groups similar buyers together.

**Q10.** True or False: In Self-supervised learning, the "labels" are generated automatically by the data's own structure, whereas in Unsupervised learning, there are no labels or pseudo-labels generated at all.

---

### Answers and Explanations

**A1.** A small portion of the data is **labeled**, and the majority is **unlabeled**. 

**A2.** Because labeling data is often **expensive, slow, or requires human experts** (like doctors labeling medical images). Using the unlabeled data helps the model learn the structure of the data and improve its performance without paying for millions of labels.

**A3.** A **reward** (positive or negative) and a **new state** of the environment.

**A4.** **False.** There is no dataset of correct actions. The agent learns by trial and error, taking actions, and seeing what rewards it gets. 

**A5.** C. The goal is to learn a policy (sequence of actions) that maximizes cumulative rewards.

**A6.** It **creates its own labels** automatically from the data using an auxiliary task (a "pretext task"). For example, it hides a word in a sentence and uses the hidden word as the label.

**A7.** B. (This is how models like BERT are trained).
- A is Unsupervised (Clustering).
- C is Reinforcement Learning.
- D is Semi-supervised Learning.

**A8.** In semi-supervised learning, you have a **few actual human-provided labels**. In self-supervised learning, you have **zero human-provided labels**; the model creates its own labels from the raw data.

**A9.** 
A) Semi-supervised
B) Self-supervised
C) Reinforcement Learning
D) Supervised
E) Unsupervised

**A10.** **True.** This is the exact boundary between the two. Unsupervised just finds structure (like clusters). Self-supervised invents a fake prediction task and generates pseudo-labels (like the missing word in a sentence) to train the model.

---
Here is the Boss Level. This is a mixed bag covering the applications (Pages 28–36), the typical algorithms, and the summary (Pages 37–38). 

Just like a real exam, it combines concepts. Let's see how you do!

---

## Round 4

**Q1. Healthcare:** The slides mention three specific applications of ML in healthcare and bioinformatics. Which of the following is **NOT** one of them?
A) Anomaly detection in medical signals (ECG, EEG)
B) Predicting disease presence from clinical variables
C) Performing automated robotic surgery
D) Genetic data analysis

**Q2. Finance:** In finance, banks use ML to predict the probability that a customer will default on a loan (their "credit score"). Which of the following is also a major financial application mentioned in the slides?
A) Predicting the weather for agricultural loans
B) Fraud detection in banking transactions
C) Optimizing hospital staff schedules
D) Generating fake stock market news

**Q3. Industry:** What is "predictive maintenance" in the context of industry and engineering?
A) Fixing a machine after it breaks down
B) Anticipating machine failures using sensors before they happen
C) Predicting the stock price of a manufacturing company
D) Grouping machines into different categories based on their color

**Q4. Web & E-commerce:** When Netflix or Amazon recommends a movie or product to you based on what similar users liked, what is this called?
A) Predictive maintenance
B) Route optimization
C) Similarity-based recommendations (Collaborative filtering)
D) Anomaly detection

**Q5. Transportation:** In transportation and logistics, ML is used for route optimization, traffic management, and demand prediction. The slides mention that **Reinforcement Learning** is a typical algorithm for this sector. Why does RL make sense for traffic/transportation?
A) Because it clusters cars into groups
B) Because it learns optimal policies (sequences of actions) to maximize rewards (like reducing travel time)
C) Because it uses a labeled dataset of the best routes
D) Because it creates fake labels from raw GPS data

**Q6. Data Analytics:** A supermarket wants to distinguish customers who frequently buy organic products from those who prefer promotions. What type of ML task is this?
A) Regression
B) Classification
C) Clustering (Customer segmentation)
D) Reinforcement Learning

**Q7. Algorithm Matching:** Match the algorithm to the type of task it is most commonly used for according to the slides:
1. Linear Regression
2. K-Means
3. SVM (Support Vector Machine)
4. PCA (Principal Component Analysis)

*Tasks:*
A) Clustering (finding groups)
B) Classification (finding boundaries)
C) Regression (predicting a continuous number)
D) Dimensionality reduction (compressing features)

**Q8. The "To Remember" Slide:** According to the summary on Page 37, what is the **key difference** between classical programming and machine learning?
A) Machine learning is always faster than classical programming.
B) In classical programming, the programmer defines all the rules, whereas in ML, the model learns the relationships from data.
C) Classical programming requires more data than machine learning.
D) Machine learning doesn't require a computer.

**Q9. The Five Types:** Name the five main types of machine learning mentioned in the "To Remember" summary. (Hint: One is Supervised, one is Unsupervised...)

**Q10. Scenario Challenge:** You are a data scientist at a telecom company. You are given a dataset of subscriber behavior (features) but you don't know which subscribers will cancel their contracts. You want to find out if there are distinct groups of at-risk customers. Which learning type are you doing?
A) Supervised
B) Unsupervised
C) Semi-supervised
D) Reinforcement

---

### Answers and Explanations

**A1. C** *(Performing automated robotic surgery)*. 
While robots do surgery, the slides specifically mention anomaly detection in medical signals, predicting disease, and genetic data analysis. 

**A2. B** *(Fraud detection in banking transactions)*. 
The slides also mention credit risk assessment and time series forecasting (interest rates/stock prices). 

**A3. B** *(Anticipating machine failures using sensors before they happen)*. 
This saves money and prevents downtime, rather than waiting for the machine to break.

**A4. C** *(Similarity-based recommendations / Collaborative filtering)*. 
The slides mention "Similarity-based recommendations (collaborative filtering, k-NN)" for Web and e-commerce.

**A5. B** *(Because it learns optimal policies to maximize rewards)*. 
RL is perfect for dynamic environments like traffic, where the agent learns a sequence of actions (a policy) to achieve a goal (like minimizing congestion). 

**A6. C** *(Clustering / Customer segmentation)*. 
Because you don't have predefined labels for the customers; you are letting the algorithm find the groups based on purchasing behavior. 

**A7.** 
1-C (Linear Regression = Regression)
2-A (K-Means = Clustering)
3-B (SVM = Classification)
4-D (PCA = Dimensionality reduction)

**A8. B**. 
As the slide says: "It is not the programmer who defines all the rules, but the model that learns the relationships."

**A9.** Supervised, Unsupervised, Semi-supervised, Reinforcement, Self-learning (Self-supervised). 

**A10. B** *(Unsupervised)*. 
You don't have the target label (who will cancel), so you are using unsupervised learning (clustering) to discover hidden structures/segments in the data. If you *did* have historical data of who canceled and who didn't, it would be Supervised.

---

You did incredibly well! You got **8 out of 10** perfectly correct. The only two you missed were **Q6** (a tricky wording trap) and **Q7** (which looks like you just mixed up the letters when matching). 

Let's break down those two so you're rock solid:

### Q6: The Tricky Trap
You chose **B (Classification)**, but the correct answer is **C (Clustering)**.
- **Why?** The word "distinguish" made you think of classification. But remember: Classification requires you to already have **labeled data** (e.g., a dataset where you already know exactly which customers are "organic buyers" and which are "promo buyers"). 
- In this scenario, the supermarket has the purchasing behavior data, but *doesn't* have pre-defined labels. They are asking the ML model to **discover** these groups from scratch. That is **Clustering** (Unsupervised). 
- *Slide check:* On page 35, it explicitly lists "Customer segmentation (clustering)" under Data Analytics. You did the exact same thing correctly in Q10, but the word "distinguish" threw you off here.

### Q7: The Letter Mix-up
You got K-Means right (A), but you mixed up the letters for the other three. Let's re-align them:
1. **Linear Regression** → **C** (Regression / predicting a continuous number)
2. **K-Means** → **A** (Clustering) — *You got this one right!*
3. **SVM (Support Vector Machine)** → **B** (Classification / finding boundaries)
4. **PCA (Principal Component Analysis)** → **D** (Dimensionality reduction / compressing features)

*(You had 1-B, 3-D, 4-C, which looks like you accidentally shifted the letters! But conceptually, you know what these algorithms do, so don't sweat it).*

---

### Everything else was flawless!
- **Q1-Q5, Q8-Q10:** Perfect. You perfectly understood predictive maintenance, collaborative filtering, why RL is used for traffic, and the exact definition of the 5 learning types.


---


1. What ML is (and how it differs from traditional programming).
2. The complete ML workflow.
3. The 5 main learning types (Supervised, Unsupervised, Semi-supervised, RL, Self-supervised).
4. The difference between them (labels vs no labels vs rewards vs self-generated).
5. Real-world applications and which algorithms belong where.

Take a break, you've earned it. When you're ready to tackle **Chapter 1, Part 2 (Probability and Statistics Refresher)**, or if you want to go through the **Typical Algorithms** (Linear Regression, SVM, etc.) mentioned in the slides before moving on, just let me know!