---
share: true
---
2026-03-11  13:41
Tags:

---

# Regularization in Scikit-Learn

## 1. Why Regularization?

When models become complex (e.g., **polynomial regression with many features**), they can **overfit** the training data.

Regularization solves this by adding a **penalty term** to the loss function.

The model now minimizes:
$$
[  
Loss = RSS + Penalty  
]
$$
Where:

- **RSS (Residual Sum of Squares)**  
    Measures prediction error.
    
$$
[  
RSS = \sum (y_i - \hat{y}_i)^2  
]
$$
- **Penalty**  
    Penalizes large coefficients.
    

### Why penalize large coefficients?

Large coefficients usually mean:

- the model is relying too heavily on certain features
    
- the model is fitting noise instead of real patterns
    

Regularization **shrinks coefficients**, which helps reduce **overfitting**.

---

# 2. Types of Regularization

## Ridge Regression (L2)

Adds penalty on **squared coefficients**.
$$
[  
Loss = RSS + \alpha \sum \beta^2  
]
$$
Properties:

- Shrinks coefficients
    
- **Does NOT eliminate features**
    
- Good when **many features contribute a little**
    

---

## Lasso Regression (L1)

Adds penalty on **absolute coefficients**.
$$
[  
Loss = RSS + \alpha \sum |\beta|  
]
$$
Properties:

- Can shrink coefficients to **exactly zero**
    
- Performs **automatic feature selection**
    
- Very useful for **high-dimensional data**
    

---

## Elastic Net

Combines **Ridge + Lasso**.
$$
[  
Loss = RSS + \alpha (L1 + L2)  
]
$$
Advantages:

- Handles correlated features better than Lasso
    
- Performs feature selection but remains stable
    

---

# 3. Example Workflow (Scikit-Learn)

Typical workflow:

```
Dataset
   ↓
Polynomial Features
   ↓
Train/Test Split
   ↓
Feature Scaling
   ↓
Regularized Model (Ridge / Lasso / ElasticNet)
   ↓
Cross Validation
   ↓
Evaluation
```

---

# 4. Data Setup

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("Advertising.csv")

X = df.drop('sales', axis=1)
y = df['sales']
```

---

# 5. Polynomial Feature Expansion

Polynomial regression creates **interaction and nonlinear features**.

Example:

Original features:

```
TV
Radio
Newspaper
```

Polynomial degree 2:

```
TV
Radio
Newspaper
TV^2
TV*Radio
TV*Newspaper
Radio^2
Radio*Newspaper
Newspaper^2
```

Code:

```python
from sklearn.preprocessing import PolynomialFeatures

polynomial_converter = PolynomialFeatures(degree=3, include_bias=False)

poly_features = polynomial_converter.fit_transform(X)
```

`degree=3` This means:

Create polynomial features **up to power 3**.

Example with one feature:

Original:

x

Degree 3 becomes:

x  
x²  
x³

---

`include_bias=False`

Normally the library adds a column of **1s**.

Example:

1  
x  
x²

The `1` corresponds to the **intercept** in regression.

But **sklearn linear models already add intercept automatically**, so we disable it.

Thus:

include_bias=False

avoids duplicate intercept.

---

# 6. Train / Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    poly_features,
    y,
    test_size=0.3,
    random_state=101
)
```

Purpose:

- Training set → fit model
    
- Test set → evaluate generalization
    

---

# 7. Feature Scaling (Very Important)

Regularization depends on **coefficient magnitude**.

If features are on different scales:

```
Income = 100000
Age = 30
```

Income will dominate the penalty.

Therefore we **standardize features**.

---

### StandardScaler

Transforms data to:

```
mean = 0
std = 1
```

Formula:
$$
[  
z = \frac{x - \mu}{\sigma}  
]
$$
Code:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

scaler.fit(X_train)

X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
```

Important rule:

```
fit → training data only
transform → training + test
```

This avoids **data leakage**!!!!!
Very important!

---

# 8. [[Why Ridge Regression|Why Ridge Regression]]

```python
from sklearn.linear_model import Ridge

ridge_model = Ridge(alpha=10)

ridge_model.fit(X_train, y_train)

test_predictions = ridge_model.predict(X_test)
```

### Evaluation

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error

MAE = mean_absolute_error(y_test, test_predictions)
MSE = mean_squared_error(y_test, test_predictions)
RMSE = np.sqrt(MSE)
```

Metrics:

|Metric|Meaning|
|---|---|
|MAE|average absolute error|
|MSE|squared error|
|RMSE|square root of MSE|

---

### Training Performance

```python
train_predictions = ridge_model.predict(X_train)

MAE = mean_absolute_error(y_train, train_predictions)
```

Comparing **train vs test error** helps detect overfitting.

---

# 9. Choosing Alpha with Cross Validation

Alpha controls regularization strength.

```
large alpha → stronger penalty
small alpha → weaker penalty
```

Instead of guessing alpha, we use **cross-validation**.
To choose the **best lamda- alpha** 

---

### RidgeCV

```python
from sklearn.linear_model import RidgeCV

ridge_cv_model = RidgeCV(
    alphas=(0.1, 1.0, 10.0)
)

ridge_cv_model.fit(X_train, y_train)

ridge_cv_model.alpha_
```

This automatically selects the best alpha.

Evaluation:

```python
test_predictions = ridge_cv_model.predict(X_test)

MAE = mean_absolute_error(y_test, test_predictions)
RMSE = np.sqrt(mean_squared_error(y_test, test_predictions))
```

---

# 10. Lasso Regression

Lasso performs **feature selection**.

```python
from sklearn.linear_model import LassoCV

lasso_cv_model = LassoCV(
    eps=0.1,
    n_alphas=100,
    cv=5
)

lasso_cv_model.fit(X_train, y_train)
```

Best alpha:

```python
lasso_cv_model.alpha_
```

Evaluation:

```python
test_predictions = lasso_cv_model.predict(X_test)

MAE = mean_absolute_error(y_test, test_predictions)
RMSE = np.sqrt(mean_squared_error(y_test, test_predictions))
```

---

### Inspect Feature Selection

```python
lasso_cv_model.coef_
```

Many coefficients will be:

```
0
```

Meaning those features were **removed**.

---

# 11. Elastic Net

Elastic Net mixes L1 and L2 penalties.

```python
from sklearn.linear_model import ElasticNetCV

elastic_model = ElasticNetCV(
    l1_ratio=[.1, .5, .7, .9, .95, .99, 1],
    tol=0.01
)

elastic_model.fit(X_train, y_train)
```

Best ratio:

```python
elastic_model.l1_ratio_
```

Evaluation:

```python
test_predictions = elastic_model.predict(X_test)

MAE = mean_absolute_error(y_test, test_predictions)
RMSE = np.sqrt(mean_squared_error(y_test, test_predictions))
```

---

### Coefficients

```python
elastic_model.coef_
```

Interpretation:

```
0 → feature removed
small → weak effect
large → strong effect
```

---

# 12. Key Comparison

|Model|Penalty|Feature Selection|
|---|---|---|
|Ridge|L2|No|
|Lasso|L1|Yes|
|ElasticNet|L1 + L2|Yes|

---

# 13. When to Use Each

### Ridge

Best when:

- many features
    
- all features useful
    
- multicollinearity exists
    

---

### Lasso

Best when:

- high dimensional data
    
- many irrelevant features
    
- need feature selection
    

---

### Elastic Net

Best when:

- many correlated features
    
- Lasso unstable
    

---

# 14. Important ML Lessons

Regularization is crucial when:

- feature space becomes large
    
- polynomial features are used
    
- dataset is small relative to features
    

Regularization helps control:

```
Bias – Variance Tradeoff
```

```
High variance → overfitting
High bias → underfitting
```

Regularization **increases bias slightly but reduces variance**.

---

# 15. Typical Modern Pipeline

In real ML pipelines:

```
Feature Engineering
↓
Polynomial / Interaction features
↓
Scaling
↓
Regularization
↓
Cross Validation
↓
Model evaluation
```

---

