---
share: true
---
2026-03-09  17:18
Tags:

---

# 1️⃣ The problem: train/test split is unstable

Normally we do this:

```
dataset
   ↓
train set (70%)
test set (30%)
```

Then:

```
train → model learns
test → evaluate performance
```

Example result:

```
RMSE = 5.1
```

But here's the problem.

If we split the data **differently**, we might get:

```
RMSE = 4.2
```

or

```
RMSE = 6.0
```

Why?

Because the **train/test split was random**.

So one split might accidentally be:

```
easy test set
```

while another might be:

```
hard test set
```

Your evaluation becomes **unstable**.

---

# 2️⃣ The idea of Cross Validation

Instead of testing the model **once**, we test it **multiple times on different splits**.

This gives a **more reliable estimate of performance**.

---

# 3️⃣ k-fold cross validation

The most common type is **k-fold CV**.

Example:

```
k = 5
```

Split data into **5 equal parts**.

```
Fold1
Fold2
Fold3
Fold4
Fold5
```

Then we train 5 models.

---

### Round 1

```
Train: Fold2 Fold3 Fold4 Fold5
Test:  Fold1
```

---

### Round 2

```
Train: Fold1 Fold3 Fold4 Fold5
Test:  Fold2
```

---

### Round 3

```
Train: Fold1 Fold2 Fold4 Fold5
Test:  Fold3
```

---

### Round 4

```
Train: Fold1 Fold2 Fold3 Fold5
Test:  Fold4
```

---

### Round 5

```
Train: Fold1 Fold2 Fold3 Fold4
Test:  Fold5
```

Now we get **5 performance scores**.

Example:

```
RMSE scores

4.8
5.1
4.9
5.2
5.0
```

Final performance:

```
mean RMSE = 5.0
```

Much more stable.

---

# 4️⃣ Why cross validation works

Each data point becomes:

```
training data → several times
test data → once
```

So the evaluation uses **the entire dataset** more efficiently.

This is especially important when datasets are **not huge**.

(Which is common in medical research.)

---

# 5️⃣ Visualization

Without CV:

```
one test split
↓
one score
↓
risky estimate
```

With CV:

```
multiple splits
↓
multiple scores
↓
average score
↓
stable estimate
```

---

# 6️⃣ Python example

Using sklearn:

```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LinearRegression

model = LinearRegression()

scores = cross_val_score(model, X, y, cv=5)

print(scores)
```

Example output:

```
[0.81, 0.84, 0.79, 0.83, 0.82]
```

Then:

```
mean = 0.818
```

---

# 7️⃣ Cross validation for hyperparameter tuning

This is where CV becomes really powerful.

Example:

You want to choose the **best polynomial degree**.

Instead of using one split:

```
degree = 1 → RMSE = 5.3
degree = 2 → RMSE = 4.9
degree = 3 → RMSE = 5.5
```

You use **cross validation**.

```
degree 1 → RMSE avg = 5.2
degree 2 → RMSE avg = 4.7
degree 3 → RMSE avg = 5.1
```

Now degree 2 clearly wins.

---

# 8️⃣ Grid Search (automatic hyperparameter tuning)

This combines **cross validation + parameter search**.

Example with LASSO:

```python
from sklearn.model_selection import GridSearchCV
from sklearn.linear_model import Lasso

param_grid = {'alpha':[0.01,0.1,1,10]}

grid = GridSearchCV(Lasso(), param_grid, cv=5)

grid.fit(X,y)
```

Output:

```
best alpha = 0.1
```

So CV helps choose the **best model settings**.

---

# 9️⃣ Important rule: CV is done on the training set

Correct workflow:

```
dataset
   ↓
train / test split
   ↓
cross validation on train
   ↓
select model
   ↓
evaluate once on test
```

Never do CV on the full dataset **after seeing the test data**.

Otherwise you leak information.

---

# 🔟 When CV is especially useful

Cross validation is most important when:

```
small dataset
many features
model tuning
```

Which describes many **medical datasets**.

---

# 1️⃣1️⃣ How it connects to your thesis

Your EMS project has something like:

```
many predictors
limited events
```

In that situation CV helps:

- evaluate models
    
- tune regularization
    
- choose predictors
    
- compare models
    

Example pipeline:

```
feature engineering
↓
LASSO
↓
cross validation
↓
choose lambda
↓
final model
```

---

# 1️⃣2️⃣ Typical values of k

Common choices:

```
k = 5
k = 10
```

Tradeoff:

|k|effect|
|---|---|
|small|faster|
|large|more accurate|

Most ML papers use:

```
5-fold CV
or
10-fold CV
```

---

# The key intuition

Cross validation asks:

> "If this model saw slightly different data, would it still perform well?"

If performance stays stable across folds → model is reliable.

---
