---
share: true
---
2026-03-18  14:25
Tags:

## 📌 Core Concept

Many machine learning models **cannot handle categorical data as strings**.

Example:

- Linear regression cannot assign coefficients to values like `"red"` or `"blue"`
    

👉 Therefore, we must convert categorical variables into **numeric form**

---

## 🔄 Solution: Dummy Variables (One-Hot Encoding)

Convert categories into binary columns:

```python
pd.get_dummies(data)
```

👉 Also known as:

- Dummy variables
    
- One-hot encoding
    

---

## 📦 Imports

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## 📂 Load Data

```python
df = pd.read_csv("../DATA/Ames_NO_Missing_Data.csv")
df.head()
```

---

## 📖 Data Description

```python
with open('../DATA/Ames_Housing_Feature_Description.txt','r') as f: 
    print(f.read())
```

---

# ⚠️ Numerical Column to Categorical

Some columns look numeric but are actually **categorical codes**

### Example: `MSSubClass`

Values:

```
20 → 1-STORY 1946 & NEWER  
30 → 1-STORY 1945 & OLDER  
...
```

👉 These numbers **do NOT represent magnitude or order**

💡 Although `30 > 20`, it does NOT mean “better” or “larger”

---

## ✅ Convert to String (Categorical)

```python
df['MS SubClass'] = df['MS SubClass'].apply(str)
```

---

# ⚠️ Dummy Variable Trap (Multicollinearity)

Example:

```python
person_state = pd.Series(['Dead','Alive','Dead','Alive','Dead','Dead'])
pd.get_dummies(person_state)
```

👉 This creates redundant columns

---

## ✅ Solution: Drop First Column

```python
pd.get_dummies(person_state, drop_first=True)
```

💡 Removes one category to avoid multicollinearity

---

# 🔍 Select Column Types

## Separate numeric and categorical features

```python
df.select_dtypes(include='object')
df_nums = df.select_dtypes(exclude='object')
df_objs = df.select_dtypes(include='object')
```

---

## Inspect

```python
df_nums.info()
df_objs.info()
```

---

# 🔄 Convert Categorical Variables

```python
df_objs = pd.get_dummies(df_objs, drop_first=True)
```

---

# 🔗 Combine Back

```python
final_df = pd.concat([df_nums, df_objs], axis=1)
final_df
```

---

# ⚠️ Final Thoughts

- The dataset now has **many more columns (e.g. 274)**
    
- More features **does NOT guarantee better performance**
    

💡 May lead to:

- Overfitting
    
- Worse model generalization
    

---

## 🔍 Feature Correlation

```python
final_df.corr()['SalePrice'].sort_values()
```

---

# 📌 Example Feature: `OverallQual`

```
10 → Very Excellent  
1 → Very Poor  
```

👉 This feature is likely **human-rated**

💡 Implication:

- It may already summarize other features
    
- Future predictions may require human input
    

---

# 💾 Save Final Dataset

```python
final_df.to_csv('../DATA/AMES_Final_DF.csv')
```

---




# 🧠 Dummy Variable Trap

## 📌 Core Idea (one sentence)

> The dummy variable trap happens when your encoded features are **perfectly predictable from each other**, causing **multicollinearity**.

---

## 🧩 Start with an Example

Original categorical variable:

```python
State = ['Alive', 'Dead']
```

### One-hot encoding:

```python
Alive   Dead
1       0
0       1
1       0
```

---

## 🚨 Where is the problem?

Look closely:

```python
Dead = 1 - Alive
```

👉 That means:

- If you know `Alive`, you automatically know `Dead`
    
- One column is **redundant**
    

---

## 🔥 Why is this bad?

### Think like a regression model:

Model tries to learn:

```python
y = β1 * Alive + β2 * Dead
```

But since:

```python
Dead = 1 - Alive
```

Substitute:

```python
y = β1 * Alive + β2 * (1 - Alive)
  = β2 + (β1 - β2) * Alive
```

👉 Now we have:

- Infinite combinations of (β1, β2) that give the SAME result
    

---

## 💥 Result

- Coefficients become **unstable**
    
- Model cannot uniquely determine weights
    
- Interpretability becomes meaningless
    

This is called:

👉 **Perfect multicollinearity**

---

## ✅ Solution: Drop One Column

```python
pd.get_dummies(data, drop_first=True)
```

Now:

```python
Dead
1
0
```

👉 Interpretation:

- `Dead = 1` → Dead
    
- `Dead = 0` → Alive (baseline)
    

---

## 🧠 Intuition (this is the key)

Think of it like:

> You don’t need both:
> 
> - “Is Alive?”
>     
> - “Is Dead?”
>     

👉 One is enough.

---

## 🎯 General Rule

If a categorical variable has:

- **k categories**
    

👉 You only need:

- **k - 1 dummy variables**
    




---

# What is `pd.concat()`?

## Core idea

`pd.concat()` combines multiple pandas objects (DataFrames or Series) along a specified axis.

You can think of it as **stacking or aligning tables together**.

---

# Two main modes

## 1. Concatenate rows (`axis=0`)

```python
pd.concat([df1, df2], axis=0)
```

- Stacks DataFrames vertically
    
- Adds more rows
    
- Columns must match (otherwise NaN appears)
    

---

## 2. Concatenate columns (`axis=1`) ← your case

```python
pd.concat([df1, df2], axis=1)
```

- Combines DataFrames side by side
    
- Adds more columns
    
- Rows are aligned by index
    

---

# Your specific usage

```python
final_df = pd.concat([df_nums, df_objs], axis=1)
```

### What’s happening:

- `df_nums`: numeric features
    
- `df_objs`: categorical features after one-hot encoding
    
- `axis=1`: combine columns
    

Result:

- A single DataFrame with all features
    
- All columns are numeric → ready for ML models
    

---

# Important detail: index alignment

`pd.concat()` aligns data by index.

Example:

```python
df1.index = [0,1]
df2.index = [1,2]

pd.concat([df1, df2], axis=1)
```

Result:

|index|df1|df2|
|---|---|---|
|0|✔|NaN|
|1|✔|✔|
|2|NaN|✔|

So if indices don’t match, you will introduce missing values.

---

# Common mistake

```python
pd.concat([df_nums, df_objs], axis=0)
```

This will:

- Stack rows instead of columns
    
- Create many NaNs because columns differ
    

---

# When to use `concat`

Use `pd.concat()` when:

- You already have separate DataFrames
    
- You just want to combine them
    
- No key-based matching is needed
    

---

# Mental model

- `axis=0`: add more observations
    
- `axis=1`: add more features
    

---

If you want, next I can explain the difference between `concat`, `merge`, and `join` — that’s where most people get confused.