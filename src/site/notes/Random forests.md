---
{"dg-publish":true,"permalink":"/random-forests/","created":"2026-11-14T13:33:27.917+01:00","updated":"2026-11-14T13:49:51.455+01:00","dg-note-properties":{}}
---

#ml 
***
###  The Overall Operation of a Random Forest🌳🌲🌴

Imagine you have a dataset where one feature is incredibly predictive (like "Income" for predicting if someone buys a yacht). 
If we just use Bagging, almost *every* tree will choose "Income" as the very first split at the root. Even though the trees are trained on different bootstrap samples, they will end up looking very similar because they all rely on that one dominant feature. If they all make the same mistakes, averaging them doesn't help much.

To fix this, Random Forests force the trees to be **decorrelated** (more different from each other).
algo:
#### 1. Bootstrapping the Data (The Bagging part)
*   Create \(M\) subsamples (with replacement) from the training set.
*   Train a decision tree on each sample.

#### 2. Random Selection of Variables
*   **At each node** of **each tree**, the algorithm does *not* look at all \(p\) features to find the best split. 
*   Instead, it randomly selects a subset of \(m\) features.
*   It tests the splits *only* on those \(m\) features and picks the best one among them.
*   If you have 100 features, at a specific node, it might only look at a random subset of $\sqrt{100} = 10$ features to make the split. 
 a tree might be forced to use a weaker feature if the strong feature wasn't randomly selected for that node. capturing different patterns in the data!
#### 3. Aggregating the Results
*   For **Regression**: Average the predictions of all \(M\) trees.
*   For **Classification**: Use **Majority Voting**.

#### The Rule of Thumb
How many features (\(m\)) should you randomly select at each node out of the total \(p\) features?
*   **For Classification:** $m \approx \sqrt{p}$ (Square root of the total features).
*   **For Regression:** $m \approx p / 3$ (One-third of the total features).

By combining **Bagging** (randomizing the rows/data) and **Feature Randomness** (randomizing the columns/features), Random Forests create a highly diverse "army" of trees that are incredibly robust against overfitting and noise.
***
### the name 🔀🌲

The name is a literal description of its two mechanisms:

1.  **"Random"**:  the two levels of randomness 
	 **Bagging** (randomly selecting rows of data with replacement) and
	 **Feature Subsampling** (randomly selecting a subset of columns/features at each node to consider for a split).
2.  **"Forest"**: This is simply because the model is an ensemble (a "forest") of many individual decision trees.

### 🔬 Is It the Only Algorithm This Random?

No, but Random Forest is uniquely defined by its *specific combination* of randomizations. many algorithms use randomness, but they use it differently:

*   **Bagging (Alone)**: Bagging only randomizes the **rows** (data samples). I
*   **Boosting (e.g., AdaBoost, Gradient Boosting)**: These methods are **sequential**, not random in the same way. Each new model is trained to correct the errors of the previous ones, using **weighted data** (AdaBoost) or **residuals/gradients** (GBM), rather than random resampling.
*   **Extremely Randomized Trees (Extra-Trees)**: This is another ensemble method that takes randomness a step further. It randomizes the **thresholds** for each feature at a node, in addition to the feature subset. So, it's even *more* random than a standard Random Forest.

So, while many algorithms use randomness, the **dual randomization of both rows and columns** is the signature of a Random Forest.

### 🚀 Are They Used a Lot?

🔀🌲 are  one of the most powerful "off-the-shelf" ML algorithms. They are praised for their:
*   **High accuracy**🎯 across a wide variety of problems.
*   **Robustness**  to overfitting and noise.
*   **Ability to handle** high-dimensional data, missing values, and both categorical and numerical features without much preprocessing.

They are a go-to choice , especially for tabular data 📊

### The Advantages of  🔀🌲

#### 1.  Reduce overfitting 
 averaging lots of decorrelated trees reduces overfitting. 

#### 2. (OOB) Error 
For every tree, about 37% of the data is left out (the Out-Of-Bag samples). 

Here is the magic trick: Because a tree never saw its OOB samples during training, we can use that tree to predict them. 
*   For **every single observation** in your dataset, you can look at all the trees that *never saw it*. You let those specific trees predict the target for that observation.
*   You then average or vote on those predictions. 
*   The error you calculate from this process is the **OOB Error**.

**cool:** It acts as a **free internal validation set**. Normally, you have to split your data into `train_test_split` to see how well your model generalizes. With Random Forests, the OOB error gives you a nearly unbiased estimate of your model's performance **without** needing to set aside a separate validation set. You can use 100% of your data for training!

#### 3. Feature Importance
Because a Random Forest has hundreds of trees, you can't easily look at it and say "Ah, Income was the most important feature." 

Instead, the algorithm tracks the **Mean Decrease in Impurity**. 
*   Every time a feature is used to split a node, it reduces the impurity (Gini or MSE).
*   The algorithm adds up all the impurity reductions caused by a specific feature across **all nodes** in **all trees**.
*   The feature that reduces impurity the most is the most important feature.

This is useful for **Feature Selection**. If you have 500 variables, the 🔀🌲 can tell you that only 20 of them matter, allowing you to drop the rest and simplify your model.

***

