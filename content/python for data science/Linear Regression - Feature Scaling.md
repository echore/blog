---
share: true
---
2025-11-07  20:28
Tags:
### Definition

**Feature scaling** is the process of transforming numerical variables so that they share a **similar range or distribution**.  
This prevents variables with large numeric ranges from dominating model training.

---

### Why It Matters

Machine learning algorithms rely on **distance** or **gradient-based optimization**.  
If features have very different scales (e.g., age = 0–100 vs. income = 0–100000),  
the algorithm may:

- Take uneven optimization steps
    
- Converge slowly or not at all
    
- Give undue weight to large-magnitude features
    

_Feature scaling makes optimization faster and more stable._
If you don't know whether you need to do the feature scaling, then just do it, there is no 'real' drawback.

---

### Common Methods
![[Pasted image 20251107203006.png|Pasted image 20251107203006.png]]
most two ways:
1. standardization Z score  which is Normal Distribution
2. normalization range 0-1

---

### Algorithms That **Need** Scaling

| Needs Scaling                                                   | Doesn’t Need Scaling ❌                     |
| --------------------------------------------------------------- | ------------------------------------------ |
| Gradient-based models (Linear/Logistic Regression, Neural Nets) | Tree-based models (Random Forest, XGBoost) |
| KNN, K-Means, PCA, SVM                                          | Naive Bayes                                |

![[Pasted image 20251107203859.png|Pasted image 20251107203859.png]]

![[Pasted image 20251107203909.png|Pasted image 20251107203909.png]]

![[Pasted image 20251107203923.png|Pasted image 20251107203923.png]]

![[Pasted image 20251107203932.png|Pasted image 20251107203932.png]]



---

# 1️⃣ The Problem: Features on Different Scales

Imagine a dataset like this:

|Feature|Example values|
|---|---|
|Age|20 – 90|
|Blood pressure|90 – 180|
|Income|20,000 – 200,000|
|Distance to hospital|0.5 – 30|

The **ranges are completely different**.

Example input row:

```
Age = 40
BloodPressure = 120
Income = 80000
Distance = 10
```

Now imagine a regression model:
$$
[  
y = \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3  
]
$$
But:

```
x1 ≈ 50
x2 ≈ 120
x3 ≈ 80000
```

The income feature dominates purely because its **numeric magnitude is huge**.

Not because it is more important.

---

# 2️⃣ What Feature Scaling Does

Feature scaling **rescales variables so they have similar ranges**.

Instead of:

```
Age = 40
Income = 80000
```

We convert them to something like:

```
Age_scaled = 0.2
Income_scaled = 0.3
```

Now the model treats features **fairly**.

---

# 3️⃣ Two Main Types of Scaling

## ① Standardization (most common)

Formula:
$$
[  
x_{scaled} =  
\frac{x - \mu}{\sigma}  
]
$$
Where

```
μ = mean
σ = standard deviation
```

This makes the feature:

```
mean = 0
std = 1
```

Example:

|Original|Scaled|
|---|---|
|100|0|
|120|1|
|80|-1|

This is called **z-score normalization**.

---

### Python example

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)
```

---

## ② Min-Max Scaling

Formula:
$$
[  
x_{scaled} =  
\frac{x - x_{min}}{x_{max} - x_{min}}  
]
$$
This converts values to:

```
0 → minimum
1 → maximum
```

Example:

|Original|Scaled|
|---|---|
|10|0|
|20|0.5|
|30|1|

Python:

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
```

---

# 4️⃣ Which scaling is better?

Most ML models prefer:

👉 **Standardization**

because many algorithms assume:

```
mean = 0
variance = 1
```

Examples:

- logistic regression
    
- linear regression
    
- ridge
    
- lasso
    
- neural networks
    
- SVM
    
- PCA
    

---

# 5️⃣ When scaling is NOT necessary

Some models **do not care about feature scale**.

Tree models only care about **splits**.

Example:

```
age > 50
```

Whether age is 50 or 0.5 after scaling doesn't matter.

Models that DON'T require scaling:

- Decision Trees
    
- Random Forest
    
- XGBoost
    
- LightGBM
    

---

# 6️⃣ Why scaling is critical for Regularization

Remember LASSO / Ridge penalty:
$$
[  
\lambda \sum |\beta|  
]
$$
If features have different scales:

```
Income: 0–100000
Age: 20–80
```

The coefficients become incomparable.

Example:

```
β_income = 0.0001
β_age = 2
```

Age looks more important but actually:

```
0.0001 × 80000 = 8
```

Income effect is bigger.

Regularization **breaks without scaling**.

So the correct pipeline is:

```
Standardize
↓
LASSO / Ridge
```

---

# 7️⃣ Another reason: gradient descent stability

Many algorithms learn using **gradient descent**.

If features have very different scales:

The optimization landscape looks like this:

```
very narrow valley
```

Gradient descent becomes:

```
slow
unstable
zig-zagging
```

Scaling makes the loss surface **rounder**, so training is faster.

---

# 8️⃣ The correct workflow (very important)

Never do this:

```
scale entire dataset
↓
train test split
```

This causes **data leakage**.

Correct workflow:

```
train test split
↓
fit scaler on train data
↓
transform train
↓
transform test using same scaler
```

Example:

```python
scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

Notice:

```
fit only on train
```

---

# 9️⃣ Real ML pipelines combine these steps

Typical ML pipeline:

```
Feature Engineering
↓
Feature Scaling
↓
Regularization / Model
```

Example in sklearn:

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Lasso

pipe = Pipeline([
    ("scaler", StandardScaler()),
    ("model", Lasso(alpha=0.1))
])

pipe.fit(X_train, y_train)
```

This prevents mistakes.

---

# 🔑 The big intuition

Feature scaling ensures:

> **model coefficients reflect importance, not measurement units**

---

# A small advanced insight (useful later)

Sometimes people scale **before polynomial features**.

Because otherwise:

```
x² explodes
```

Example:

```
TV budget = 200
TV² = 40000
```

Scaling first keeps polynomial features stable.

---

