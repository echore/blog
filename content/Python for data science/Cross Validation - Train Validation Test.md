---
share: true
---
2026-03-18  14:54
Tags:

# Introduction to Cross Validation
---

## Imports

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## Data Example

```python
df = pd.read_csv("../DATA/Advertising.csv")
df.head()
```

---

# Train | Test Split Procedure

## Workflow

0. Clean and adjust data as necessary for `X` and `y`
    
1. Split data into Train/Test for both `X` and `y`
    
2. Fit/Train scaler on training `X` data
    
3. Scale `X` test data
    
4. Create model
    
5. Fit/Train model on `X_train`
    
6. Evaluate model on `X_test` by creating predictions and comparing to `y_test`
    
7. Adjust parameters as necessary and repeat steps 5 and 6
    

---

## Create `X` and `y`

```python
X = df.drop('sales', axis=1)
y = df['sales']
```

---

## Train Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=101
)
```

---

## Scale Data

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
scaler.fit(X_train)

X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
```

Note:

- The scaler is fit only on `X_train`
    
- Then the same fitted scaler is used to transform both `X_train` and `X_test`
    

---

## Create Model

```python
from sklearn.linear_model import Ridge

model = Ridge(alpha=100)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

Poor alpha choice on purpose:

```python
model = Ridge(alpha=100)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

---

## Evaluation

```python
from sklearn.metrics import mean_squared_error

mean_squared_error(y_test, y_pred)
```

---

## Adjust Parameters and Re-evaluate

```python
model = Ridge(alpha=1)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

---

## Another Evaluation

```python
mean_squared_error(y_test, y_pred)
```

Observation:

- `alpha=1` performs much better than `alpha=100` in this example
    
- This process can be repeated until satisfied with performance metrics
    

Note:

- `RidgeCV` can automate this for Ridge regression
    
- The purpose here is to understand the general cross-validation process for any model
    

---

# Train | Validation | Test Split Procedure

This is also called a **hold-out set** approach.

Key idea:

- Do not adjust parameters based on the final test set
    
- Use the final test set only for reporting final expected performance
    

---

## Workflow

0. Clean and adjust data as necessary for `X` and `y`
    
1. Split data into Train/Validation/Test for both `X` and `y`
    
2. Fit/Train scaler on training `X` data
    
3. Scale evaluation data
    
4. Create model
    
5. Fit/Train model on `X_train`
    
6. Evaluate model on evaluation data by creating predictions and comparing to `y_eval`
    
7. Adjust parameters as necessary and repeat steps 5 and 6
    
8. Get final metrics on test set
    
    - not allowed to go back and adjust after this
        

---

## Create `X` and `y`

```python
X = df.drop('sales', axis=1)
y = df['sales']
```

---

## Split Twice: Train | Validation | Test

```python
from sklearn.model_selection import train_test_split

# 70% of data is training data, set aside other 30%
X_train, X_OTHER, y_train, y_OTHER = train_test_split(
    X, y, test_size=0.3, random_state=101
)

# Remaining 30% is split into evaluation and test sets
# Each is 15% of the original data size
X_eval, X_test, y_eval, y_test = train_test_split(
    X_OTHER, y_OTHER, test_size=0.5, random_state=101
)
```

---

## Scale Data

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
scaler.fit(X_train)

X_train = scaler.transform(X_train)
X_eval = scaler.transform(X_eval)
X_test = scaler.transform(X_test)
```

---

## Create Model

```python
from sklearn.linear_model import Ridge

# Poor Alpha Choice on purpose!
model = Ridge(alpha=100)
model.fit(X_train, y_train)
y_eval_pred = model.predict(X_eval)
```

---

## Evaluation

```python
from sklearn.metrics import mean_squared_error

mean_squared_error(y_eval, y_eval_pred)
```

---

## Adjust Parameters and Re-evaluate

```python
model = Ridge(alpha=1)
model.fit(X_train, y_train)
y_eval_pred = model.predict(X_eval)
```

---

## Another Evaluation

```python
mean_squared_error(y_eval, y_eval_pred)
```

---

## Final Evaluation

After this step, parameters should no longer be changed.

```python
y_final_test_pred = model.predict(X_test)
mean_squared_error(y_test, y_final_test_pred)
```

---

# Cross Validation with `cross_val_score`

```python
X = df.drop('sales', axis=1)
y = df['sales']
```

---

## Train Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=101
)
```

---

## Scale Data

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
scaler.fit(X_train)

X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
```

---

## Create Model

```python
from sklearn.linear_model import Ridge

model = Ridge(alpha=100)
```

---

## Run Cross Validation

```python
from sklearn.model_selection import cross_val_score

# SCORING OPTIONS:
# https://scikit-learn.org/stable/modules/model_evaluation.html

scores = cross_val_score(
    model,
    X_train,
    y_train,
    scoring='neg_mean_squared_error',
    cv=5
)
scores
```

Note:

- `cv=5` means 5-fold cross validation
    
- For error metrics like MSE, scikit-learn returns the negative version, so lower error corresponds to a larger negative score
    
- To interpret MSE more naturally, take the absolute value of the mean
    

---

## Average CV Score

```python
abs(scores.mean())
```

---

## Adjust Model Based on Metrics

```python
model = Ridge(alpha=1)

scores = cross_val_score(
    model,
    X_train,
    y_train,
    scoring='neg_mean_squared_error',
    cv=5
)
```

---

## Mean CV Error

```python
abs(scores.mean())
```

---

## Final Evaluation

```python
# Need to fit the model first!
model.fit(X_train, y_train)

y_final_test_pred = model.predict(X_test)
mean_squared_error(y_test, y_final_test_pred)
```

---

# Cross Validation with `cross_validate`

## Difference from `cross_val_score`

`cross_validate` differs from `cross_val_score` in two ways:

1. It allows specifying multiple metrics for evaluation
    
2. It returns a dictionary containing:
    
    - fit times
        
    - score times
        
    - test scores
        
    - optionally training scores and fitted estimators
        

---

## Return Values

### For single metric evaluation

If `scoring` is a string, callable, or `None`, the keys will be:

```python
['test_score', 'fit_time', 'score_time']
```

### For multiple metric evaluation

The returned dictionary contains keys like:

```python
['test_<scorer1_name>', 'test_<scorer2_name>', 'test_<scorer...>', 'fit_time', 'score_time']
```

### Training Scores

- `return_train_score=False` by default
    
- This saves computation time
    
- To evaluate training scores too, set `return_train_score=True`
    

---

## Create `X` and `y`

```python
X = df.drop('sales', axis=1)
y = df['sales']
```

---

## Train Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=101
)
```

---

## Scale Data

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
scaler.fit(X_train)

X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
```

---

## Create Model

```python
from sklearn.linear_model import Ridge

model = Ridge(alpha=100)
```

---

## Run `cross_validate`

```python
from sklearn.model_selection import cross_validate

# SCORING OPTIONS:
# https://scikit-learn.org/stable/modules/model_evaluation.html

scores = cross_validate(
    model,
    X_train,
    y_train,
    scoring=['neg_mean_absolute_error', 'neg_mean_squared_error', 'max_error'],
    cv=5
)
scores
```

---

## View Results

```python
pd.DataFrame(scores)
```

```python
pd.DataFrame(scores).mean()
```

---

## Adjust Model Based on Metrics

```python
model = Ridge(alpha=1)

scores = cross_validate(
    model,
    X_train,
    y_train,
    scoring=['neg_mean_absolute_error', 'neg_mean_squared_error', 'max_error'],
    cv=5
)

pd.DataFrame(scores).mean()
```

---

## Final Evaluation

```python
# Need to fit the model first!
model.fit(X_train, y_train)

y_final_test_pred = model.predict(X_test)
mean_squared_error(y_test, y_final_test_pred)
```

---

# Summary

## Train/Test Split

- Simple
    
- Fast
    
- Good starting point
    
- But model tuning may depend too much on one split
    

## Train/Validation/Test Split

- Separates tuning from final testing
    
- Test set stays untouched until the end
    
- More reliable than only train/test
    

## `cross_val_score`

- Performs cross-validation directly
    
- Good for one evaluation metric
    
- Returns an array of scores
    

## `cross_validate`

- More flexible than `cross_val_score`
    
- Supports multiple metrics
    
- Also returns fit time and score time
    




---

# `cross_val_score` vs `cross_validate`

## 1. Core difference

|Function|Purpose|
|---|---|
|`cross_val_score`|Simple CV → returns **only scores**|
|`cross_validate`|Advanced CV → returns **detailed results**|

---

# 2. `cross_val_score`

## What it does

```python
scores = cross_val_score(model, X, y, cv=5, scoring='neg_mean_squared_error')
```

## Output

```python
array([-10.2, -9.8, -11.0, -10.5, -9.9])
```

👉 Only gives:

- test scores for each fold
    

---

## When to use

- You only care about **one metric**
    
- You want something quick and simple
    

---

# 3. `cross_validate`

## What it does

```python
scores = cross_validate(
    model,
    X,
    y,
    cv=5,
    scoring=['neg_mean_squared_error', 'neg_mean_absolute_error']
)
```

## Output

```python
{
  'test_neg_mean_squared_error': [...],
  'test_neg_mean_absolute_error': [...],
  'fit_time': [...],
  'score_time': [...]
}
```

👉 Returns a dictionary

---

## What extra info you get

- Multiple metrics
    
- Fit time
    
- Score time
    
- (optional) training scores
    

---

# 4. Side-by-side comparison

|Feature|`cross_val_score`|`cross_validate`|
|---|---|---|
|Multiple metrics|❌|✅|
|Fit time|❌|✅|
|Score time|❌|✅|
|Train score|❌|✅ (optional)|
|Output type|array|dict|

---

# 5. Subtle but important

## `cross_val_score`

```python
scores.mean()
```

👉 directly usable

---

## `cross_validate`

```python
pd.DataFrame(scores).mean()
```

👉 need to extract from dict

---

# 6. When YOU should use which

Given your project (ML + model comparison):

### Use `cross_val_score` when:

- quick check of model performance
    
- tuning one metric (e.g. AUC)
    

### Use `cross_validate` when:

- comparing multiple metrics
    
- analyzing model behavior
    
- debugging performance
    

---

# 7. One line intuition

- `cross_val_score` = **just give me the score**
    
- `cross_validate` = **give me everything about training + evaluation**
    

---

