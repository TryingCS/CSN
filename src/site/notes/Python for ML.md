---
{"dg-publish":true,"permalink":"/python-for-ml/","created":"2026-11-02T22:55:33.594+01:00","updated":"2026-11-06T17:40:45.985+01:00","dg-note-properties":{}}
---

#python #ml 

The core insight: **all ML code in this course is 4 things:**
1. **NumPy** — math on arrays (fast, vectorized)
2. **pandas** — load and inspect tabular data
3. **Matplotlib** — see what's happening
4. **sklearn** — the same 3 methods (`fit` / `predict` / `score`) on every model

---

# Part 1 — NumPy: The Foundation

NumPy is what you'll use to **implement algorithms from scratch** (logistic regression, AdaBoost). Everything here matters.

## 1.1 Creating arrays

```python
import numpy as np

# From a Python list
a = np.array([1, 2, 3, 4])
print(a, a.shape)              # (4,) — 1D, 4 elements

# 2D array (matrix) — outer brackets = rows, inner = columns
M = np.array([[1, 2, 3],
              [4, 5, 6]])
print(M.shape)                 # (2, 3) — 2 rows, 3 cols

# Special arrays
z = np.zeros((3, 2))           # 3 rows × 2 cols of 0.0
o = np.ones((2, 1))            # 2 rows × 1 col of 1.0
r = np.arange(0, 10, 2)        # [0, 2, 4, 6, 8]
lin = np.linspace(0, 1, 5)     # [0, 0.25, 0.5, 0.75, 1.0]
```

## 1.2 Shape — the #1 source of bugs

```python
v = np.array([1, 2, 3])            # shape (3,)  ← 1D, NOT a column
col = v.reshape(-1, 1)             # shape (3, 1) ← column vector
row = v.reshape(1, -1)             # shape (1, 3) ← row vector

print(v.shape, col.shape, row.shape)
```

**Why this matters in your labs:**
- Logistic regression: `w` must be shape `(n_features, 1)` so `X @ w` gives `(n_samples, 1)`.
- `y` must be reshaped to `(m, 1)` or sometimes you'll see shape errors when doing `y - A` (element-wise).

Rule of thumb:
- **Features `X`**: always 2D → `(n_samples, n_features)`
- **Weights `w`**: 2D → `(n_features, 1)`
- **Target `y`**: either `(m,)` or `(m, 1)`, pick one and stick with it

## 1.3 Indexing and slicing

```python
M = np.array([[10, 20, 30],
              [40, 50, 60],
              [70, 80, 90]])

print(M[0, 0])       # 10   — row 0, col 0 (0-indexed!)
print(M[1, :])       # [40 50 60]       — entire row 1
print(M[:, 2])       # [30 60 90]       — entire col 2
print(M[0:2, 1:3])   # [[20 30], [50 60]] — sub-matrix
print(M[-1, -1])     # 90   — last element

# Boolean masking (super useful)
mask = M > 40
print(M[mask])       # [50 60 70 80 90]  — only values > 40
```

## 1.4 Element-wise arithmetic (broadcasting)

```python
a = np.array([1, 2, 3])
b = np.array([10, 20, 30])

print(a + b)         # [11 22 33]
print(a * b)         # [10 40 90]       ← element-wise, NOT matrix mult
print(a ** 2)        # [1 4 9]
print(2 * a)         # [2 4 6]
print(a + 10)        # [11 12 13]       ← scalar broadcasts
```

**Broadcasting** = NumPy stretches smaller arrays to match bigger ones:

```python
M = np.array([[1, 2, 3],
              [4, 5, 6]])      # (2, 3)
row = np.array([10, 20, 30])   # (3,)

print(M + row)   # adds [10, 20, 30] to EACH row
# [[11, 22, 33],
#  [14, 25, 36]]
```

This is why in your labs you can write `X @ w + b` when `b` is a scalar — NumPy broadcasts `b` across all rows.

## 1.5 Matrix multiplication — the `@` operator

**This is the most important NumPy operation for ML.** The `@` symbol = matrix multiplication. `*` = element-wise.

```python
A = np.array([[1, 2],
              [3, 4]])      # (2, 2)
B = np.array([[5, 6],
              [7, 8]])      # (2, 2)

print(A * B)   # element-wise: [[5, 12], [21, 32]]
print(A @ B)   # matrix:      [[19, 22], [43, 50]]
```

**Shape rules for `@`:** inner dimensions must match.
```
(2, 3) @ (3, 4)  →  (2, 4)   ✓
(3,)   @ (3,)    →  scalar    ✓  (dot product)
(2, 3) @ (2, 3)  →  ERROR     ✗  inner 3 ≠ 2
```

**In your labs:**
```python
# Linear regression: predicted = X @ coef + intercept
# Logistic regression: z = X @ w + b     (X: (m, n), w: (n, 1) → (m, 1))
# Gradients: dw = (1/m) * X.T @ (A - y)  (X.T: (n, m), (A-y): (m, 1) → (n, 1))
```

`.T` = transpose. `X.T @ something` is how you sum gradients across samples.

## 1.6 The functions you'll actually call

```python
a = np.array([1.0, -2.0, 3.0, -4.0])

np.sum(a)            # -2.0
np.mean(a)           # -0.5
np.sum(a ** 2)       # 30.0     (sum of squares)
np.abs(a)            # [1. 2. 3. 4.]
np.exp(a)            # [2.718, 0.135, 20.086, 0.018]   ← e^x
np.log(np.abs(a))    # natural log
np.sign(a)           # [ 1. -1.  1. -1.]     ← used in L1 gradient!
np.clip(a, -1, 1)    # [-1. -1.  1. -1.]     ← caps values
np.where(a > 0, 1, -1)  # [1 -1 1 -1]         ← if/else on arrays
```

**`np.where`** is the "vectorized if/else":
```python
# y in {0, 1} → y in {-1, +1}   (AdaBoost needs this!)
y = np.array([0, 1, 1, 0])
y_signed = np.where(y == 1, 1, -1)   # [-1, 1, 1, -1]
```

**`np.clip`** prevents overflow:
```python
# sigmoid(z) = 1/(1+exp(-z)) blows up when z is very negative
# because exp(-(-500)) = exp(500) = inf → overflow
z = np.clip(z, -500, 500)   # safe range
```

## 1.7 Randomness with reproducibility

```python
np.random.seed(42)                  # old-style
rng = np.random.default_rng(42)     # modern style

print(np.random.rand(3))            # uniform [0, 1)
print(rng.normal(0, 1, size=3))     # normal(μ=0, σ=1)

# Bootstrap sample (Random Forest needs this)
indices = rng.integers(0, len(X), size=len(X))
X_boot = X[indices]
```

## 1.8 Vectorization — why not just use loops?

```python
# Slow (Python loop)
total = 0
for x in arr:
    total += x ** 2

# Fast (NumPy vectorized)
total = np.sum(arr ** 2)
```

NumPy operates in C. A `for` loop on a 1M-element array is ~100× slower than the vectorized version. **In from-scratch implementations, always prefer vectorized operations.**

Example from your lab — the logistic gradient:
```python
# Slow:
dw = np.zeros((n, 1))
for i in range(m):
    for j in range(n):
        dw[j] += X[i, j] * (A[i] - y[i])
dw /= m

# Fast (same result):
dw = (1/m) * X.T @ (A - y)
```

## 🧪 Exercise — try these

```python
# 1. Create a (5, 3) array of random numbers
M = np.random.rand(5, 3)

# 2. Compute its shape
print(M.shape)   # should print (5, 3)

# 3. Create a weight vector w of shape (3, 1) of zeros
w = np.zeros((3, 1))

# 4. Compute X @ w → what shape do you expect?
result = M @ w
print(result.shape)   # should be (5, 1)

# 5. What does (M @ w).shape[0] give you?   → 5 (number of samples)
```

If those ran without error, you're ready.

---

# Part 2 — pandas: Data Tables

You'll use pandas to **load and explore** data, then convert to NumPy for from-scratch code.

## 2.1 Series vs DataFrame

- **Series** = 1D column with an index
- **DataFrame** = 2D table of Series

```python
import pandas as pd

# Series
s = pd.Series([10, 20, 30], name="scores")
print(s)
# 0    10
# 1    20
# 2    30

# DataFrame
df = pd.DataFrame({
    "experience": [1.1, 1.3, 1.5],
    "salary": [39343, 46205, 37731]
})
print(df)
```

## 2.2 Loading and inspecting

```python
df = pd.read_csv("salary_data.csv")

df.head()             # first 5 rows
df.head(10)           # first 10
df.tail()             # last 5

df.info()             # column types, non-null counts
df.describe()         # numeric summary (count, mean, std, min, quartiles, max)

df.shape              # (30, 2) — 30 rows, 2 cols
df.columns.tolist()   # ['YearsExperience', 'Salary']
df.dtypes             # data types per column
```

**In your lab**: `df.info()` tells you if there are missing values (any "non-null" count less than total). `df.describe()` tells you the scale of each feature — crucial to spot the need for normalization.

## 2.3 Selecting columns and rows

```python
# Columns
df["YearsExperience"]              # Series (1D)
df[["YearsExperience", "Salary"]]  # DataFrame (2D) — note double brackets

# Rows by index
df.iloc[0]              # first row (position-based)
df.iloc[0:5]            # first 5 rows
df.iloc[:, 0]           # all rows, first column

# Rows by label
df.loc[0, "Salary"]     # value at row index 0, column "Salary"

# Conditional filter
df[df["Salary"] > 60000]          # rows where salary > 60000
df[(df["Salary"] > 60000) & (df["YearsExperience"] > 5)]   # AND with &
df[(df["Salary"] > 100000) | (df["YearsExperience"] < 2)]  # OR with |
```

**`.iloc` vs `.loc`:** `iloc` uses integer positions, `loc` uses index labels. For fresh DataFrames from CSV, they're usually identical — but be careful after filtering.

## 2.4 The correlation matrix (PW1)

```python
df.corr()               # Pearson correlation between all numeric columns
```

The resulting matrix: `1.0` on the diagonal, values in `[-1, 1]` off-diagonal. A correlation like `0.97` between experience and salary is *very strong positive linear* — strong justification for linear regression.

## 2.5 Class distribution (PW2)

```python
y = pd.Series([0, 0, 1, 1, 1, 0])
y.value_counts()        # 1    3
                        # 0    3
                        # dtype: int64

y.value_counts(normalize=True)   # proportions
```

**Why this matters:** imbalanced classes → need `stratify=y` in `train_test_split`.

## 2.6 Converting between pandas and NumPy

```python
# DataFrame → NumPy
X_np = df.values                     # everything as float64
X_np = df[["YearsExperience"]].values   # only one column
y_np = df["Salary"].values

# NumPy → DataFrame
df2 = pd.DataFrame(X_np, columns=["a", "b"])
```

**In your labs:**
- Linear regression: sklearn accepts pandas DataFrame **or** NumPy — either works.
- From-scratch code: convert `.values` first, then do math with NumPy.

## 2.7 Missing values

```python
df.isnull().sum()        # count missing per column
df = df.dropna()         # drop rows with any NaN
df = df.fillna(0)        # or fill with 0
```

In PW2 with `fetch_openml`, some datasets have `"?"` encoded as strings. Pattern:
```python
df = df.replace("?", np.nan)
df = df.apply(pd.to_numeric, errors="coerce")   # coerce non-numeric to NaN
df = df.dropna()
```

## 🧪 Exercise

```python
df = pd.DataFrame({"x": [1, 2, 3, 4], "y": [10, 20, 30, 40]})
df["z"] = df["x"] * 2              # create new column
print(df[df["z"] > 4])              # filter rows
print(df.corr())                    # correlation matrix
print(df["y"].values)               # → array([10, 20, 30, 40])
```

---

# Part 3 — Matplotlib: Plotting

Three plot types cover everything in your labs.

## 3.1 Scatter plot (PW1: salary vs experience)

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(8, 5))
plt.scatter(df["YearsExperience"], df["Salary"],
            color="steelblue", alpha=0.7, label="Data")
plt.xlabel("Years of Experience")
plt.ylabel("Salary")
plt.title("Salary vs Experience")
plt.legend()
plt.grid(alpha=0.3)
plt.show()
```

- `alpha` = transparency (0 = invisible, 1 = solid)
- `figsize=(width_inches, height_inches)`
- `plt.show()` at the end of the cell

## 3.2 Line plot (PW1 & PW2: convergence curves, depth study)

```python
depths = [1, 2, 3, 4, 5]
train_acc = [0.80, 0.92, 0.97, 0.99, 1.00]
test_acc  = [0.78, 0.90, 0.94, 0.93, 0.91]

plt.figure(figsize=(8, 5))
plt.plot(depths, train_acc, "o-", label="Train")     # o- = circles + line
plt.plot(depths, test_acc,  "s-", label="Test")      # s- = squares + line
plt.xlabel("max_depth")
plt.ylabel("Accuracy")
plt.title("Decision Tree: train vs test")
plt.legend()
plt.grid(alpha=0.3)
plt.show()
```

**Format strings** (the `"o-"` thing):
- `o` = circle marker, `s` = square, `^` = triangle, `.` = dot
- `-` = solid line, `--` = dashed, `:` = dotted, `-.` = dash-dot
- `r`, `g`, `b` = colors (red, green, blue)

Example: `"ro--"` = red circles, dashed line.

## 3.3 Confusion matrix as heatmap (PW2)

```python
import seaborn as sns
from sklearn.metrics import confusion_matrix

cm = confusion_matrix(y_test, y_pred)

sns.heatmap(cm, annot=True, fmt="d", cmap="Blues",
            xticklabels=["Pred 0", "Pred 1"],
            yticklabels=["Actual 0", "Actual 1"])
plt.title("Confusion matrix")
plt.ylabel("Actual")
plt.xlabel("Predicted")
plt.show()
```

- `annot=True` = show numbers in cells
- `fmt="d"` = integer format
- `cmap="Blues"` = color scheme

## 3.4 ROC curves

```python
from sklearn.metrics import roc_curve, roc_auc_score

fpr, tpr, _ = roc_curve(y_test, y_proba)

plt.plot(fpr, tpr, label=f"AUC = {roc_auc_score(y_test, y_proba):.3f}")
plt.plot([0, 1], [0, 1], "k:", label="Random")   # diagonal reference
plt.xlabel("False Positive Rate")
plt.ylabel("True Positive Rate")
plt.legend()
plt.show()
```

## 3.5 Subplots (when you want multiple panels)

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 4))   # 1 row, 2 cols

axes[0].plot([1, 2, 3], [1, 4, 9])
axes[0].set_title("Panel A")

axes[1].plot([1, 2, 3], [9, 4, 1])
axes[1].set_title("Panel B")

plt.tight_layout()
plt.show()
```

Note: with subplots you use `axes[i].plot(...)` instead of `plt.plot(...)`.

## 🧪 Exercise

Plot `y = x²` for `x` from 0 to 10, then overplot `y = x³` on the same axes with a different color and a legend. If you can do that from memory, you have everything.

---

# Part 4 — scikit-learn: The Universal Pattern

Every sklearn model has the **same three methods**. Once you know them, you know all of them.

## 4.1 The `fit / predict / score` pattern

```python
from sklearn.linear_model import LinearRegression

# 1. Create the model (with hyperparameters)
model = LinearRegression()

# 2. Fit on training data
model.fit(X_train, y_train)

# 3. Predict on new data
y_pred = model.predict(X_test)

# 4. Score (default metric: R² for regression, accuracy for classification)
print(model.score(X_test, y_test))
```

That's **identical** for `Ridge`, `Lasso`, `RandomForestClassifier`, `GradientBoostingClassifier`, `LogisticRegression`, etc. Learn this once, use it 20 times.

## 4.2 Special methods per model type

**All models:**
- `.fit(X, y)` — train
- `.predict(X)` — predict class or value
- `.score(X, y)` — accuracy / R²

**Classifiers add:**
- `.predict_proba(X)` — probabilities `[P(class 0), P(class 1)]` — shape `(n_samples, 2)`

**Trees add:**
- `.feature_importances_` — importance per feature (RandomForest, DecisionTree)

**Models add:**
- `.coef_`, `.intercept_` — learned parameters (LinearRegression, LogisticRegression)

**Example:**
```python
rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)

# Probabilities for class 1 — needed for ROC
y_proba = rf.predict_proba(X_test)[:, 1]

# Feature importances
print(rf.feature_importances_)
```

## 4.3 train_test_split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.3,       # 30% test
    random_state=42,     # reproducibility
    stratify=y           # keep class ratios equal
)
```

**Parameter significance:**
- `random_state=42` = seed. Without it, every run gives a different split → impossible to debug.
- `stratify=y` = keep class distribution equal in train/test (essential for imbalanced data, like PW2).

## 4.4 Preprocessing

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_train_scaled = scaler.fit_transform(X_train)   # learn min/max FROM TRAIN, apply to train
X_test_scaled  = scaler.transform(X_test)        # apply SAME min/max to test (no refit!)
```

**Critical rule:** `fit_transform` on train, `transform` on test. Never `fit` on test — that would leak test information into training.

## 4.5 Metrics (both labs)

```python
from sklearn.metrics import (
    mean_squared_error, r2_score,            # regression
    accuracy_score, confusion_matrix,
    classification_report,
    roc_curve, roc_auc_score                 # classification
)

# Regression
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

# Classification
acc = accuracy_score(y_test, y_pred)
cm = confusion_matrix(y_test, y_pred)
print(classification_report(y_test, y_pred))

# ROC / AUC — needs probabilities, not classes!
fpr, tpr, thresholds = roc_curve(y_test, y_proba)
auc = roc_auc_score(y_test, y_proba)
```

**MSE vs R²:**
- **MSE** — average squared error. Units = target². Lower is better. Not interpretable directly.
- **R²** — fraction of variance explained. 1.0 = perfect, 0.0 = no better than predicting the mean. Standard for regression.

**accuracy vs confusion_matrix vs classification_report:**
- `accuracy_score` — one number, fraction correct. Easy but hides class imbalance problems.
- `confusion_matrix` — 2×2 grid showing TP/TN/FP/FN. Shows *which* errors you make.
- `classification_report` — precision, recall, F1 per class. Best summary.

## 4.6 Loading datasets

```python
# PW2 — built-in, no download needed
from sklearn.datasets import load_breast_cancer
data = load_breast_cancer()
X = data.data              # array (569, 30)
y = data.target            # array (569,)
data.feature_names         # list of 30 names
data.target_names          # ['malignant', 'benign']

# PW1 — downloaded from OpenML
from sklearn.datasets import fetch_openml
heart = fetch_openml(name="heart-disease", version=1, as_frame=True)
df = heart.frame           # DataFrame
```

## 4.7 The models you need

| Lab | Model | One line |
|---|---|---|
| PW1 | `LinearRegression()` | `model.fit(X, y)` |
| PW1 | `Ridge(alpha=…)` / `Lasso(alpha=…)` / `ElasticNet(alpha=…)` | same API |
| PW2 | `DecisionTreeClassifier(max_depth=…, random_state=42)` | same API |
| PW2 | `RandomForestClassifier(n_estimators=100, random_state=42)` | same API |
| PW2 | `GradientBoostingClassifier(n_estimators=100, random_state=42)` | same API |
| PW2 | `LogisticRegression(max_iter=1000)` | same API |
| PW2 | `StackingClassifier(estimators=…, final_estimator=…, cv=5)` | same API |

Every single one: `.fit(X, y)`, `.predict(X)`, `.score(X, y)`. That's it.

## 🧪 Exercise

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score

X, y = load_iris(return_X_y=True)
X_tr, X_te, y_tr, y_te = train_test_split(X, y, test_size=0.3, random_state=42, stratify=y)

clf = DecisionTreeClassifier(random_state=42)
clf.fit(X_tr, y_tr)
print("Accuracy:", clf.score(X_te, y_te))
print("Predicted classes:", clf.predict(X_te[:5]))
```

Once that runs, you've used the whole sklearn API.

---

# Part 5 — From-Scratch Patterns (Revisited with Numbers)

Now that you know NumPy and sklearn, here's how the from-scratch code fits together. **Read these as math being translated to NumPy.**

## 5.1 Sigmoid — the gateway to classification

**Formula:** σ(z) = 1 / (1 + e⁻ᶻ)

```python
def sigmoid(z):
    z = np.clip(z, -500, 500)
    return 1 / (1 + np.exp(-z))
```

**Why it works:**
- Input `z` = any real number
- Output = probability in (0, 1)
- If `z = 0`: `1/(1+1) = 0.5`
- If `z = +∞`: `1/(1+0) ≈ 1`
- If `z = −∞`: `1/(1+∞) ≈ 0`

**Try:**
```python
print(sigmoid(np.array([-2, 0, 2])))   # [0.119 0.5 0.881]
```

## 5.2 Log loss (cross-entropy)

**Formula:** J = −(1/m) Σ [y·log(ŷ) + (1−y)·log(1−ŷ)]

```python
def compute_loss(y, y_pred):
    m = len(y)
    y_pred = np.clip(y_pred, 1e-15, 1 - 1e-15)   # avoid log(0)
    return -(1/m) * np.sum(y * np.log(y_pred) + (1 - y) * np.log(1 - y_pred))
```

**Why the clip?** `log(0) = -inf` → breaks everything. Clipping to `1e-15` keeps it finite.

**Interpretation:** It's the negative log-likelihood of the true labels under the predicted probabilities. Perfect predictions → 0. Worst predictions → large.

## 5.3 Gradient descent

**Loop:**
1. Compute predictions
2. Compute loss
3. Compute gradients (how much to change each parameter)
4. Update parameters
5. Repeat

```python
def gradient_descent(X, y, w, b, alpha=0.1, num_iters=1000, compute_fn=None):
    costs = []
    for i in range(num_iters):
        cost, dw, db = compute_fn(X, y, w, b)
        w = w - alpha * dw       # ← MINUS because we're minimizing
        b = b - alpha * db
        costs.append(cost)
    return w, b, costs
```

**The update rule** is always: **parameter = parameter − learning_rate × gradient**. If you accidentally write `+`, cost goes up → divergent. That's your #1 bug.

**Reading a convergence curve:**
- Cost goes **down and flattens** = good
- Cost goes **up** = learning rate too big, or sign flipped
- Cost **flat from the start** = learning rate too small, or something is broken
- Cost **NaN** = `log(0)` or overflow — clip your inputs

## 5.4 The AdaBoost weight update (PW2)

The tricky part: **labels must be {−1, +1}**, not {0, 1}.

```python
# Wrong: exp(-alpha * y * y_pred) with y in {0, 1}
# → when y=0, the term is exp(0) = 1 (no change to weight) — broken!

# Right: remap first
y_signed = np.where(y == 1, 1, -1)
w_new = w * np.exp(-alpha * y_signed * y_pred)
w_new = w_new / w_new.sum()
```

**Why does the formula work?**
- Correct prediction: `y·ŷ = +1` → `exp(−α)` < 1 → **weight shrinks**
- Wrong prediction: `y·ŷ = −1` → `exp(+α)` > 1 → **weight grows**

So the next stump focuses on previously misclassified samples. That's the whole idea of boosting.

**The alpha formula:**
```python
alpha = 0.5 * np.log((1 - err) / err)
```
- `err = 0.1` (good stump) → `0.5 · log(9) ≈ 1.10` → large positive
- `err = 0.5` (random) → `0.5 · log(1) = 0` → contributes nothing
- `err = 0.9` (worse than random) → negative → would *hurt* the ensemble

---

# Part 6 — The Gotchas


## 6.1 Shape mismatches (the #1 bug)

```python
X = np.random.rand(100, 5)     # (100, 5)
w = np.zeros((5, 1))           # (5, 1)

z = X @ w                      # (100, 1) ✓

w = np.zeros(5)                # (5,)   ← WRONG
z = X @ w                      # (100,)  ← works! but shape is 1D now
A = sigmoid(z)                 # (100,)
y = np.random.randint(0, 2, 100)   # (100,)
# Everything still works... until you do something needing (m, 1)
```

**Rule:** **Always verify shapes right before using an array.** Add print statements:
```python
print("X:", X.shape, "w:", w.shape, "A:", A.shape, "y:", y.shape)
```

If you see a shape error you can't explain, add prints. Problem solved 80% of the time.

## 6.2 The `(m,)` vs `(m, 1)` confusion

```python
a = np.array([1, 2, 3])           # (3,)     1D
b = np.array([[1], [2], [3]])     # (3, 1)   2D column

print(a.shape, b.shape)
# print(a + b)   # works by broadcasting → (3, 3) — SURPRISING!
```

If you're mixing shapes and getting surprising results, do `a.reshape(-1, 1)` or `b.reshape(-1)` explicitly.

## 6.3 Copy vs view

```python
a = np.array([1, 2, 3])
b = a               # b is the SAME object
b[0] = 100
print(a)            # [100 2 3]  ← a changed!

b = a.copy()        # explicit copy
b[0] = 999
print(a)            # unchanged
```

In pandas:
```python
df2 = df.copy()     # if you plan to modify, always copy
```


## 6.4 `==` vs `is`

```python
a == b              # value equality (what you want 99% of the time)
a is b              # identity (same object in memory)
```

Only use `is` for `None`:
```python
if x is None:
    ...
```

## 6.6 Indexing from 0

```python
arr = [10, 20, 30]
arr[0]     # 10  ← first element
arr[-1]    # 30  ← last element
arr[1:3]   # [20, 30]  ← 1, 2 (NOT 3!)
```

Slicing `[start:stop]` includes `start`, excludes `stop`..

## 6.7 Truth value of NumPy arrays

```python
a = np.array([1, 2, 3])
# if a:                # ERROR! Ambiguous truth value
if a.any():            # ✓  if ANY element is truthy
if a.all():            # ✓  if ALL elements are truthy
if a.sum() > 0:        # ✓  explicit check
```

## 6.8 Passing pandas Series where array is expected

Sometimes works, sometimes doesn't. Safe habit:
```python
X = df[["feature"]].values   # always .values for from-scratch code
y = df["target"].values
```

## 6.9 `random_state` everywhere

Every sklearn model and split with randomness should get `random_state=42`. Without it, results change on every run → impossible to compare or debug. **Rule: if it's a randomness-using function, pass `random_state=42`.**

## 6.10 Print shapes early and often

When a from-scratch function breaks:

```python
def compute_cost(X, y, w, b):
    print(f"X: {X.shape}, w: {w.shape}, b: {b}, y: {y.shape}")
    z = X @ w + b
    print(f"z: {z.shape}")
    A = sigmoid(z)
    print(f"A: {A.shape}")
    ...
```


---

# Cheat Sheet — One Page

## NumPy
```python
np.array([1,2,3])          # 1D array
np.zeros((3, 1))           # 3×1 zeros
np.ones((2, 3))            # 2×3 ones
np.arange(0, 10, 2)        # [0, 2, 4, 6, 8]
np.linspace(0, 1, 5)       # [0, 0.25, 0.5, 0.75, 1.0]

A.shape                    # dimensions
A.reshape(-1, 1)           # column vector
A.T                        # transpose

A + B                      # element-wise
A * B                      # element-wise
A @ B                      # matrix multiplication
A ** 2                     # element-wise square

np.sum(A), np.mean(A)
np.exp(A), np.log(np.clip(A, 1e-15, None))
np.abs(A), np.sign(A)
np.clip(A, lo, hi)
np.where(cond, a, b)       # vectorized if-else
np.random.rand(3, 3)
np.random.default_rng(42)
```

## pandas
```python
pd.read_csv("file.csv")
df.head(), df.info(), df.describe()
df.shape, df.columns, df.dtypes
df["col"], df[["col1", "col2"]]
df[df["col"] > 5]                 # filter
df.iloc[0], df.loc[0, "col"]
df.corr()
df["col"].values                  # → NumPy
df.isnull().sum()
df.dropna()
pd.Series([1,2,3]).value_counts()
```

## Matplotlib
```python
plt.figure(figsize=(8, 5))
plt.plot(x, y, "o-", label="label")
plt.scatter(x, y, alpha=0.7)
plt.xlabel("x"), plt.ylabel("y"), plt.title("title")
plt.legend(), plt.grid(alpha=0.3)
plt.show()

sns.heatmap(cm, annot=True, fmt="d", cmap="Blues")
```

## sklearn — universal API
```python
from sklearn.model_selection import train_test_split
X_tr, X_te, y_tr, y_te = train_test_split(
    X, y, test_size=0.3, random_state=42, stratify=y)

from sklearn.preprocessing import MinMaxScaler
sc = MinMaxScaler()
X_tr = sc.fit_transform(X_tr)
X_te = sc.transform(X_te)

model = AnyModel(..., random_state=42)
model.fit(X_tr, y_tr)
y_pred = model.predict(X_te)
y_proba = model.predict_proba(X_te)[:, 1]   # classifiers only
score = model.score(X_te, y_te)

from sklearn.metrics import (
    accuracy_score, confusion_matrix, classification_report,
    mean_squared_error, r2_score,
    roc_curve, roc_auc_score)
```

## From-scratch
```python
def sigmoid(z):
    z = np.clip(z, -500, 500)
    return 1 / (1 + np.exp(-z))

# Cost
A = sigmoid(X @ w + b)
A = np.clip(A, 1e-15, 1 - 1e-15)
cost = -(1/m) * np.sum(y*np.log(A) + (1-y)*np.log(1-A))

# Gradients
dz = A - y
dw = (1/m) * (X.T @ dz)
db = (1/m) * np.sum(dz)

# Update
w = w - alpha * dw
b = b - alpha * db
```

---
# even noobier

## 2. Types
```python
age = 25                    # int   (whole number)
salary = 45000.50           # float (decimal number)
first_name = "Sarah"        # str   (text, in quotes — single or double)
is_married = False          # bool  (True or False, capital T/F)

print(type(age))            # <class 'int'>
```

---

## 3. Comments 
```python
# This line is a comment. Python ignores it.

```
---

## 4. Arithmetic 

```python
print(2 + 3)      # 5     addition
print(10 - 4)     # 6     subtraction
print(6 * 7)      # 42    multiplication
print(10 / 3)     # 3.333 division (ALWAYS gives a decimal)
print(10 // 3)    # 3     floor division (drops the decimal)
print(10 % 3)     # 1     modulo (remainder)
print(2 ** 10)    # 1024  power
```

**Order of operations** follows math

---

## 5. Printing things together

```python

print(f"Hello, {name}! You are {age} years old.")# Hello, Sarah! You are 30 years old.
print(f"Age squared: {age ** 2}")  # Age squared: 900
```

**f-strings** — put `f` before the quote, and wrap variables in `{curly braces}`. 

---

## 6. Strings — text values

```python
greeting = "hello"
name = "world"

# Join strings with +
print(greeting + " " + name)     # hello world

# Length
print(len(greeting))             # 5

# Upper / lower
print(greeting.upper())          # HELLO
print(greeting.lower())          # hello

# Split on a character
print("a,b,c".split(","))        # ['a', 'b', 'c']

# Replace
print("I love cats".replace("cats", "dogs"))   # I love dogs
```

**You'll use string methods when:**
- Reading CSVs with weird formats.
- Building plot titles and print statements.

---

## 7. `if` / `else` — make decisions

```python
age = 20

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

**Syntax :**
- The `if` line **ends with a colon** `:`.
- The body **must be indented** (4 spaces — Jupyter does this automatically).
- Dedented code runs after the `if` block.

### `elif` — chain multiple conditions

```python
score = 85

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("F")
```

**Output:** `B`

### The comparison operators

```python
x == 5       # equal to         (TWO equals signs!)
x != 5       # not equal to
x > 5        # greater than
x < 5        # less than
x >= 5       # greater or equal
x <= 5       # less or equal
```


### Combining conditions

```python
age = 25
has_license = True

if age >= 18 and has_license:
    print("Can drive")

if age < 18 or not has_license:
    print("Cannot drive")
```

---

## 8. Lists — ordered collections

A list holds **multiple values** in order.

```python
scores = [85, 92, 78, 96, 88]

print(scores)              # [85, 92, 78, 96, 88]
print(len(scores))         # 5 (number of items)
print(scores[0])           # 85  (first — index 0!)
print(scores[0:3])         # [85, 92, 78]  (index 0, 1, 2 — NOT 3!)

# Add at the end
scores.append(100)
print(scores)              # [85, 92, 78, 96, 88, 100]

# Sum / min / max
print(sum(scores))         # 539
print(max(scores))         # 100
print(min(scores))         # 78
```

**Key facts:**
- Indexing starts at **0**. First element is `[0]`, second is `[1]`.
- Slicing `[start:stop]` includes start, **excludes** stop.
- Lists **can** be modified after creation (mutable).

### Empty list — used as an accumulator

```python
results = []               # empty list

```

every loop that collects results starts with `results = []`.

---

## 9. Loops

### `for` loop — iterate over items

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

**Output:**
```
apple
banana
cherry
```

Read it as: *"for each item in the list, call it `fruit`, do the following."*

### `for` loop over numbers

```python
for i in range(5):
    print(i)
```


`range(5)` produces 0, 1, 2, 3, 4 (five numbers, starting at 0). If you want 1 to 5: `range(1, 6)`.

### Doing something with each item

```python
numbers = [10, 20, 30]
total = 0

for n in numbers:
    total = total + n

print(total)                # 60
```

==This is the pattern: **start with an accumulator (`total = 0`), loop, update, print after the loop**==
### Same with a list — collect results

```python
numbers = [10, 20, 30]
doubled = []                # empty list

for n in numbers:
    doubled.append(n * 2)

print(doubled)              # [20, 40, 60]
```

**This is the exact pattern from your lab:**

```python
train_acc = []              # collect train accuracies
test_acc  = []              # collect test accuracies

for depth in [1, 2, 3, 4, 5]:
    # (imaginary code that trains a model at this depth)
    train_acc.append(0.90)  # pretend result
    test_acc.append(0.85)
```

### `for` with an index (when you need it)

```python
names = ["Alice", "Bob", "Charlie"]

for i, name in enumerate(names):
    print(f"{i}: {name}")
```

**Output:**
```
0: Alice
1: Bob
2: Charlie
```

`enumerate` gives you both the index and the value — useful when you need to know the position.

### `while` loop — repeat until a condition is false

```python
i = 0
while i < 5:
    print(i)
    i = i + 1     # ← must update, or infinite loop!
```

---

## 10. Functions — reusable blocks

A function is a **named block of code** you can call by name.

```python
def greet():
    print("Hello!")

greet()     # Hello!
greet()     # Hello!
```

- `def` starts the definition.
- `greet()` **calls** it (the parentheses are what "runs" it).

### Function with a parameter

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")     # Hello, Alice!
greet("Bob")       # Hello, Bob!
```

`name` is a **parameter** — it's filled in when you call the function.

### Function that **returns** a value

```python
def add(a, b):
    return a + b

result = add(3, 5)
print(result)      # 8
```

- `return` sends a value **back** to the caller.
- Without `return`, the function returns `None` (nothing usable).
- **`print` shows something on screen. `return` gives a value back.** They are not the same.

### Side-by-side: `print` vs `return`

```python
def f1(a, b):
    print(a + b)          # shows 8, but f1(3, 5) is None

def f2(a, b):
    return a + b          # shows nothing, but f2(3, 5) is 8

x = f1(3, 5)              # prints 8
print("x is:", x)         # x is: None    ← because no return

y = f2(3, 5)              # prints nothing
print("y is:", y)         # y is: 8
```

**For your labs: functions that compute something (accuracy, error, gradient) should `return`.** Functions that draw a plot can just run — that's fine.

### Function with default values

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")                 # Hello, Alice!
greet("Bob", "Hi")             # Hi, Bob!
greet("Eve", greeting="Hey")   # Hey, Eve!
```

Default parameters have `=` in the `def` — this is where you use a single `=` in a non-assignment context.

### A real example from your lab

```python
def sigmoid(z):
    import numpy as np
    z = np.clip(z, -500, 500)
    return 1 / (1 + np.exp(-z))
```

Read it as:
- `def sigmoid(z):` — define a function called `sigmoid` taking one input `z`.
- `return ...` — give back the computed value.

You'll call it like `sigmoid(0)` → returns `0.5`.

---

## 11. Dictionaries — key → value pairs

Like a mini database. You look things up by name (key), not position.

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "Paris",
}

print(person["name"])     # Alice
print(person["age"])      # 30

# Add a key
person["job"] = "Engineer"
print(person)             # {'name': 'Alice', 'age': 30, 'city': 'Paris', 'job': 'Engineer'}

# Iterate over keys
for key in person:
    print(key, "=", person[key])
```

**Where this appears in your lab:**

```python
models = {
    "DecisionTree": clf,
    "RandomForest": rf,
    "GradBoost": gb,
}

for name, m in models.items():
    acc = m.score(X_test, y_test)
    print(f"{name}: {acc:.3f}")
```

`models.items()` gives pairs `(name, model)` — one per loop iteration. This is the **exact pattern** from your Part 6.

---

## 12. Importing — using libraries

Python by itself doesn't have `numpy` or `pandas` loaded. You `import` them.

```python
import numpy as np              # load numpy, rename to "np" for short

# Now use them with the short name:
x = np.array([1, 2, 3])
```

**Import specific functions from a library:**

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import accuracy_score

model = LinearRegression()
acc = accuracy_score(y_true, y_pred)
```

`from X import Y` means "grab `Y` from `X` directly, no prefix needed."

**You'll see this dozens of times in your labs.** It's the same idea each time.

### Standard imports for your labs

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import accuracy_score, confusion_matrix
```

Run this once at the top of your notebook, and those names are available in every cell.

---

## 13. Common errors


### `TypeError: can only concatenate str (not "int") to str`
Trying to mix types.
```python
age = 30
print("Age: " + age)      # ERROR: can't add str + int
print("Age: " + str(age)) # Fix: convert
print(f"Age: {age}")      # Or better: f-string
```

### `IndexError: list index out of range`
You asked for an item that doesn't exist.
```python
scores = [85, 92, 78]
print(scores[10])         # IndexError — only indices 0, 1, 2 exist
```

### `KeyError: 'salary'`
You asked a dictionary for a key it doesn't have.
```python
person = {"name": "Alice"}
print(person["salary"])   # KeyError
```
**Fix:** check the key exists, or use `person.get("salary", 0)` (returns default).

### `ModuleNotFoundError: No module named 'sklearn'`
The library isn't installed. **Fix:** `pip install scikit-learn` in a terminal, then restart the kernel.

---

## 14. Putting it all together — a small program

Here's a tiny but complete program using **everything above**. Read it line by line:

```python
# Data: a list of (years_experience, salary) pairs
data = [(1.1, 39343), (2.0, 43525), (3.0, 60150), (5.0, 66029)]

# Function: predict salary using a rule (this is our "model")
def predict_salary(years, base=30000, per_year=8000):
    return base + years * per_year

# Loop: compute predictions for each row
predictions = []
for years, actual_salary in data:
    predicted = predict_salary(years)
    predictions.append(predicted)

# Loop: compute mean absolute error
total_error = 0
for (years, actual), predicted in zip(data, predictions):
    error = abs(actual - predicted)
    total_error += error

mean_error = total_error / len(data)
print(f"Mean absolute error: ${mean_error:.2f}")
```

**What each part does:**
- `data = [(1.1, 39343), ...]` — a list of tuples (pairs).
- `def predict_salary(...)` — a function with two default parameters.
- `for years, actual_salary in data:` — loop, unpack each tuple into two names.
- `predictions.append(predicted)` — collect results.
- `for (years, actual), predicted in zip(data, predictions):` — loop over two lists side by side.
- `abs(...)` — absolute value (magnitude, drops the sign).
- `f"...${mean_error:.2f}"` — format as 2 decimal places.

Try running it. Then **change** `per_year=8000` to `10000` — see how the error changes. That's the whole game: small changes, see what happens.

---

## 15. Now: how this bridges to NumPy

**NumPy is just "lists that do math better."**

Side by side:

```python
# --- Plain Python: sum of squares ---
nums = [1, 2, 3, 4]
total = 0
for n in nums:
    total = total + n ** 2
print(total)             # 30

# --- NumPy: sum of squares ---
import numpy as np
nums = np.array([1, 2, 3, 4])
print(np.sum(nums ** 2))  # 30
```

**The trade-off:**
- Plain Python list: flexible, but **slow** for math (each element is a full Python object).
- NumPy array: **fast** for math, but all elements must be the same type.

**For your labs:** everything you do with plain Python lists works with NumPy arrays too — `len(arr)`, indexing `arr[0]`, slicing `arr[0:3]`. The difference is **NumPy's math is vectorized** — `arr * 2` doubles every element at once, no loop.

```python
import numpy as np

a = np.array([1, 2, 3, 4])
print(a + 10)          # [11 12 13 14]  ← adds 10 to every element
print(a * 2)           # [ 2  4  6  8]  ← doubles every element
print(a ** 2)          # [ 1  4  9 16]  ← squares every element
```

No loops needed. **One operation on the whole array.** That's the whole point of NumPy.

**Matrix multiplication** — `@`, the operator for "matrix times matrix":

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
print(A @ B)           # [[19 22], [43 50]]
```

You don't need to know how it computes — just **recognize** that `@` means matrix multiply. You'll see it in every from-scratch ML line (`X @ w + b`).

---

## 16. Practice set

```python

# 2. Create a variable `name` = "Alice" and `age` = 30.
# Print: "Alice is 30 years old."  (use an f-string)


# 3. Create a list `scores` with [90, 85, 92, 78].
# Print the length and the first element.


# 4. If `temp = 15`, print "Cold" if temp < 20, else "Warm".


# 5. Loop over [1, 2, 3, 4, 5], print each number squared.


# 6. Define a function `double(x)` that returns x * 2.
# Call it with 7 and print the result.


# 7. Loop over the list `names = ["Alice", "Bob"]` and print "Hello, {name}!".


# 8. Create a dictionary with keys "name" and "age" and print each.

```python
# 1
age = 25
print(age)

# 2
name = "Alice"
age = 30
print(f"{name} is {age} years old.")

# 3
scores = [90, 85, 92, 78]
print(len(scores))    # 4
print(scores[0])      # 90

# 4
temp = 15
if temp < 20:
    print("Cold")
else:
    print("Warm")

# 5
for n in [1, 2, 3, 4, 5]:
    print(n ** 2)

# 6
def double(x):
    return x * 2

print(double(7))      # 14

# 7
names = ["Alice", "Bob"]
for name in names:
    print(f"Hello, {name}!")

# 8
person = {"name": "Alice", "age": 30}
for key in person:
    print(key, "=", person[key])
```


Repetition beats cramming.

---

## 17. tl;dr


```python
# 1. Assign and compute
total = 0
for n in [1, 2, 3]:
    total = total + n

# 2. Define a function that returns a value
def square(x):
    return x ** 2

# 3. If/else
if score >= 0.9:
    print("great")

# 4. Append to a list
results = []
results.append(42)

# 5. Import and use
import numpy as np
a = np.array([1, 2, 3])
```

---

