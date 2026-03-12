---
share: true
---
2026-03-12  14:28
Tags:

---

# 1. Why Encoding Is Needed

Suppose you have a variable:

|transport_mode|
|---|
|ambulance|
|helicopter|
|car|

A model **cannot read text**, so we must convert it to numbers.

This process is called **categorical encoding**.

---

# 2. Integer Encoding

Integer encoding simply assigns a number to each category.

Example:

|transport_mode|encoded|
|---|---|
|ambulance|0|
|helicopter|1|
|car|2|

Python example:

```python
from sklearn.preprocessing import LabelEncoder

encoder = LabelEncoder()
data['transport_mode_encoded'] = encoder.fit_transform(data['transport_mode'])
```

Result:

```
ambulance → 0
car → 1
helicopter → 2
```

---

## The Problem with Integer Encoding

Many models will interpret these numbers as **ordered values**.

Meaning the model thinks:

```
helicopter (2) > car (1) > ambulance (0)
```

This implies **distance and ranking**, which may not exist.

Example:

```
helicopter - ambulance = 2
```

But this **difference has no meaning**.

So integer encoding can **mislead models**.

---

# 3. Dummy Variables (One-Hot Encoding)

Instead of assigning numbers, we create **separate binary columns**.

Example:

|transport_mode|ambulance|helicopter|car|
|---|---|---|---|
|ambulance|1|0|0|
|helicopter|0|1|0|
|car|0|0|1|

Each column answers a **yes/no question**.

```
Is transport helicopter?
Is transport ambulance?
Is transport car?
```

This avoids fake ordering.

---

Python example:

```python
pd.get_dummies(data['transport_mode'])
```

or

```python
from sklearn.preprocessing import OneHotEncoder
```

---

# 4. Why We Drop One Column (Dummy Trap)

You might see something like:

|ambulance|helicopter|
|---|---|
|1|0|
|0|1|
|0|0|

Here we **removed the "car" column**.

Why?

Because if we know:

```
ambulance = 0
helicopter = 0
```

then it must be **car**.

Keeping all columns introduces **perfect multicollinearity**.

So many libraries use:

```python
drop_first=True
```

Example:

```python
pd.get_dummies(data, drop_first=True)
```

---

# 5. When to Use Each Method

### Use Dummy Variables (most common)

Good for:

- Linear regression
    
- Logistic regression
    
- LASSO / Ridge
    
- Neural networks
    
- SVM
    

Basically **most models**.

---

### Integer Encoding Works For

Tree models:

- Random Forest
    
- XGBoost
    
- Decision Trees
    

Because trees don't rely on distances.

They split like:

```
transport_mode == helicopter
```

not

```
transport_mode > car
```

---

# 7. A Small Trick Many People Don't Know

If a variable has **too many categories**, dummy encoding explodes.

Example:

```
ZIP code
doctor ID
hospital ID
```

You might get **thousands of columns**.

Solutions include:

- frequency encoding
    
- target encoding
    
- embedding methods
    

But that's more advanced.

---

# 8. Quick Summary

|Method|Idea|Problem|
|---|---|---|
|Integer encoding|category → number|fake ordering|
|Dummy variables|binary columns|more features|

Most tabular ML uses **dummy encoding**.

---

💡 Since you're doing **LASSO and logistic models**, dummy encoding is the **correct approach**.
