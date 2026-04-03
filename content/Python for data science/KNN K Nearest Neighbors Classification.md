---
share: true
---
2026-04-02 13:40
Tags:

---
Source Notebook: `/Users/liyachen/Documents/fang/UNZIP_FOR_NOTEBOOKS_FINAL/12-K-Nearest-Neighbors/00-KNN-Classification.ipynb`

# KNN -  K Nearest Neighbors - Classification

To understand KNN for classification, we'll work with a simple dataset representing gene expression levels. Gene expression levels are calculated by the ratio between the expression of the target gene (i.e., the gene of interest) and the expression of one or more reference genes (often household genes). This dataset is synthetic and specifically designed to show some of the strengths and limitations of using KNN for Classification.

More info on gene expression: https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/gene-expression-level

## Imports

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

## Data

```python
df = pd.read_csv('../DATA/gene_expression.csv')
```

```python
df.head()
```

```text
   Gene One  Gene Two  Cancer Present
0       4.3       3.9               1
1       2.5       6.3               0
2       5.7       3.9               1
3       6.1       6.2               0
4       7.4       3.4               1
```

```python
sns.scatterplot(x='Gene One',y='Gene Two',hue='Cancer Present',data=df,alpha=0.7)
```

![[assets/images/KNN K Nearest Neighbors Classification Cell 07 Output 02.png|assets/images/KNN K Nearest Neighbors Classification Cell 07 Output 02.png]]

```python
sns.scatterplot(x='Gene One',y='Gene Two',hue='Cancer Present',data=df)
plt.xlim(2,6)
plt.ylim(3,10)
plt.legend(loc=(1.1,0.5))
```

![[assets/images/KNN K Nearest Neighbors Classification Cell 08 Output 02.png|assets/images/KNN K Nearest Neighbors Classification Cell 08 Output 02.png]]

## Train|Test Split and Scaling Data

```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
```

```python
X = df.drop('Cancer Present',axis=1)
y = df['Cancer Present']
```

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```

```python
scaler = StandardScaler()
```

```python
scaled_X_train = scaler.fit_transform(X_train)
scaled_X_test = scaler.transform(X_test)
```

```python
from sklearn.neighbors import KNeighborsClassifier
```

```python
knn_model = KNeighborsClassifier(n_neighbors=1)
```

```python
knn_model.fit(scaled_X_train,y_train)
```

```text
KNeighborsClassifier(n_neighbors=1)
```

# Understanding KNN and Choosing K Value

```python
full_test = pd.concat([X_test,y_test],axis=1)
```

```python
len(full_test)
```

```text
900
```

```python
sns.scatterplot(x='Gene One',y='Gene Two',hue='Cancer Present',
                data=full_test,alpha=0.7)
```

![[assets/images/KNN K Nearest Neighbors Classification Cell 21 Output 02.png|assets/images/KNN K Nearest Neighbors Classification Cell 21 Output 02.png]]

## Model Evaluation

```python
y_pred = knn_model.predict(scaled_X_test)
```

```python
from sklearn.metrics import classification_report,confusion_matrix,accuracy_score
```

```python
accuracy_score(y_test,y_pred)
```

```text
0.8922222222222222
```

```python
confusion_matrix(y_test,y_pred)
```

```text
array([[420,  50],
       [ 47, 383]], dtype=int64)
```

```python
print(classification_report(y_test,y_pred))
```

```text
              precision    recall  f1-score   support

           0       0.90      0.89      0.90       470
           1       0.88      0.89      0.89       430

    accuracy                           0.89       900
   macro avg       0.89      0.89      0.89       900
weighted avg       0.89      0.89      0.89       900
```

## Elbow Method for Choosing Reasonable K Values

**NOTE: This uses the test set for the hyperparameter selection of K.**

```python
test_error_rates = []

for k in range(1,30):
    knn_model = KNeighborsClassifier(n_neighbors=k)
    knn_model.fit(scaled_X_train,y_train) 
   
    y_pred_test = knn_model.predict(scaled_X_test)
    
    test_error = 1 - accuracy_score(y_test,y_pred_test)
    test_error_rates.append(test_error)
```

```python
plt.figure(figsize=(10,6),dpi=200)
plt.plot(range(1,30),test_error_rates,label='Test Error')
plt.legend()
plt.ylabel('Error Rate')
plt.xlabel("K Value")
```

```text
Text(0.5, 0, 'K Value')
```

![[assets/images/KNN K Nearest Neighbors Classification Cell 30 Output 02.png|assets/images/KNN K Nearest Neighbors Classification Cell 30 Output 02.png]]

## Full Cross Validation Grid Search for K Value

### Creating a Pipeline to find K value

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import GridSearchCV

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('knn', KNeighborsClassifier())
])

param_grid = {
    'knn__n_neighbors': list(range(1, 31))
}

grid = GridSearchCV(pipe, param_grid, cv=5)
grid.fit(X_train, y_train)
```


---

# 🧠 Step 1: What problem are we actually solving?

You want to do **three things together**:

1. Scale your data
    
2. Train a KNN model
    
3. Find the best `k`
    

Now ask yourself:

> ❓ If I do these separately… what could go wrong?

---

# 🚨 Step 2: The _wrong_ way (very common beginner mistake)

```python
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)

grid = GridSearchCV(KNeighborsClassifier(), param_grid, cv=5)
grid.fit(X_train_scaled, y_train)
```

Looks fine, right?

But think deeper:

### ❗ Problem: Data leakage

Inside CV, the model is supposed to behave like this:

```
Fold 1:
    train on subset A
    validate on subset B
```

BUT your scaler was fit on **ALL X_train** already.

So:

> The validation fold has “seen” information from itself.

That’s cheating.

---

# 🧠 Step 3: So what should happen instead?

Let’s think like a clean ML pipeline:

For EACH fold:

```
1. Take training fold
2. Fit scaler ONLY on this fold
3. Transform training fold
4. Train model
5. Transform validation fold using SAME scaler
6. Evaluate
```

👉 This must happen **inside every fold**

---

# 🔥 Step 4: This is exactly why Pipeline exists

Now look at your code again:

```python
pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('knn', KNeighborsClassifier())
])
```

This is not just “writing steps”.

This is saying:

> “These steps must ALWAYS happen together, in this order, safely.”

---

# ⚙️ Step 5: What GridSearchCV does with Pipeline

Now this line:

```python
grid = GridSearchCV(pipe, param_grid, cv=5)
```

Think of it like:

> “Try different k values, and for EACH one, run the ENTIRE pipeline correctly across folds.”

---

# 🧪 What actually happens internally

For each `k`:

For each fold:

```
train_fold → scaler.fit()
train_fold → scaler.transform()
train_fold → knn.fit()

val_fold → scaler.transform()
val_fold → knn.predict()
```

---

# 🧩 Step 6: Why this syntax (`knn__n_neighbors`)?

```python
param_grid = {
    'knn__n_neighbors': list(range(1, 31))
}
```

This looks weird at first.

But think:

Pipeline = multiple layers

```
Pipeline
 ├── scaler
 └── knn
       └── n_neighbors
```

So:

```
knn__n_neighbors
```

means:

> “Go inside step `knn`, change parameter `n_neighbors`”

---




---

# 🧠 Step 1: What does “best k” actually mean?

After this:

```python
grid.fit(X_train, y_train)
```

You now have:

```python
grid.best_params_
grid.best_estimator_
```

👉 Important:

> “Best k” = best **on cross-validation**, not on real unseen data yet

---

# 🎯 Step 2: What should we do next?

Ask yourself:

> ❓ Have we evaluated on true unseen data?

If not → **we’re not done**

---

# ✅ Step 3: Use the best model on test data

```python
best_model = grid.best_estimator_

y_pred = best_model.predict(X_test)
```

Then evaluate:

```python
from sklearn.metrics import classification_report, confusion_matrix

print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

---

# 🧠 Why this step matters

Think of it like:

|Stage|Purpose|
|---|---|
|CV (GridSearch)|choose best k|
|Test set|simulate real-world performance|

👉 If you skip test evaluation → you don’t know if your model generalizes

---

# 🔥 Step 4: What’s inside `best_estimator_`?

This is important conceptually.

```python
best_model
```

is actually:

```text
Pipeline(
    scaler = fitted StandardScaler,
    knn = KNN with best k
)
```

👉 So when you call:

```python
best_model.predict(X_test)
```

it automatically:

```text
X_test → scaler.transform → knn.predict
```

No extra work needed.

---

# 🧩 Step 5: Optional but powerful — inspect performance vs k

You can also analyze:

```python
grid.cv_results_
```

Example:

```python
import pandas as pd

results = pd.DataFrame(grid.cv_results_)
results[['param_knn__n_neighbors', 'mean_test_score']]
```

This helps you see:

> Is performance stable? or very sensitive to k?

---
