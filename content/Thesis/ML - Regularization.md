---
share: true
---
2026-03-09  16:58
Tags:[[Technical Literacy|Technical Literacy]]


---

# 1️⃣ The Core Problem: Overfitting

Imagine we have a dataset:

```
patients: 200
features: 491
```

This is actually very close to your EMS dataset.

Now think about what linear regression does.

[  
y = \beta_0 + \beta_1x_1 + \beta_2x_2 + ... + \beta_{491}x_{491}  
]

The model will try to find **β coefficients** that minimize error.

But if we have **too many features**, the model can do something dangerous:

👉 memorize noise instead of learning real patterns.

Example:

```
feature: ambulance ID
feature: timestamp minute
feature: random missing indicator
```

These might accidentally correlate with the outcome in training data.

The model learns them → **great training accuracy**

But in new data → **fails badly**.

This is **overfitting**.

---

# 2️⃣ Regularization = controlling model complexity

Regularization adds a **penalty** to the regression.

Instead of minimizing just:
$$

[  
\text{Loss} = \sum (y - \hat{y})^2  
]
$$
we minimize:
$$
[  
\text{Loss} = \sum (y - \hat{y})^2 + \text{penalty}  
]
$$
The penalty discourages **large coefficients**.

Intuition:

> The model should only use a feature if it **really helps prediction**.

---

# 3️⃣ Why big coefficients are suspicious

Suppose your model becomes:

```
y = 0.2x1 + 0.3x2 + 0.1x3
```

This looks stable.

But an overfit model might become:

```
y = 120x1 − 95x2 + 210x3 − 340x4 + ...
```

Huge coefficients usually mean:

👉 the model is **bending itself to fit noise**.

Regularization prevents this.

---

# 4️⃣ Two main types of regularization

You’ll see these everywhere:

|Method|Name|
|---|---|
|L2|Ridge regression|
|L1|LASSO regression|

---

# 5️⃣ Ridge Regression (L2 regularization)

Penalty:
$$
[  
\lambda \sum \beta_i^2  
]
$$
So the full objective becomes:
$$
[  
\text{Loss} =  
\sum (y-\hat y)^2 + \lambda \sum \beta_i^2  
]
$$
Meaning:

Large coefficients are punished **quadratically**.

Effect:

```
β values shrink toward 0
```

Example:

Before:

```
[3.5, 2.1, -4.0, 0.8]
```

After ridge:

```
[2.4, 1.6, -2.8, 0.5]
```

Important:

👉 coefficients **rarely become exactly zero**

So Ridge **keeps all features**, but shrinks them.

---

# 6️⃣ LASSO (L1 regularization)

Penalty:
$$
[  
\lambda \sum |\beta_i|  
]
$$
Now the loss is:
$$
[  
\text{Loss} =  
\sum (y-\hat y)^2 + \lambda \sum |\beta_i|  
]
$$
Effect:

Some coefficients become **exactly zero**.

Example:

Before:

```
[3.5, 2.1, -4.0, 0.8]
```

After LASSO:

```
[2.2, 0, -1.7, 0]
```

This means:

```
feature2 removed
feature4 removed
```

So LASSO does:

👉 **automatic feature selection**

---

# 7️⃣ Why LASSO is popular for high-dimensional data

This is why people suggested it for your project.

If you have:

```
491 features
```

LASSO might select:

```
12 useful features
```

and remove the rest.

This gives:

```
better interpretability
less overfitting
simpler model
```

---

# 8️⃣ Geometric intuition (super famous ML idea)

Imagine a map of coefficient values.

Without regularization:

```
solution anywhere
```

With Ridge:

```
circle constraint
```

With LASSO:

```
diamond constraint
```

Because the diamond has corners, the solution often lands exactly at:

```
β = 0
```

That’s why LASSO creates **sparse models**.

---

# 9️⃣ What λ (lambda) controls

λ controls **strength of regularization**.

Small λ:

```
almost normal regression
```

Large λ:

```
heavy penalty
very small coefficients
```

Example:

|λ|effect|
|---|---|
|0|normal regression|
|0.1|mild shrink|
|1|strong shrink|
|10|extreme shrink|

Choosing λ is usually done with:

👉 **cross-validation**

---

# 🔟 Code example

Example in sklearn:

### Ridge

```python
from sklearn.linear_model import Ridge

model = Ridge(alpha=1.0)
model.fit(X_train, y_train)
```

---

### LASSO

```python
from sklearn.linear_model import Lasso

model = Lasso(alpha=0.1)
model.fit(X_train, y_train)
```

(`alpha` = λ)

---

# 🔑 The big intuition

Regularization says:

> "Simple models are more trustworthy than complex ones unless the data strongly proves otherwise."

This idea is deeply connected to:

👉 **Occam's razor**

