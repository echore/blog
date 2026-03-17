---
share: true
---
2026-03-16  11:34
Tags:

---

# Dealing with Missing Data

## Overview

In real-world datasets, **missing values (NaN)** are extremely common. Before building machine learning models, we must **clean and handle missing data**.

Important points:

- There is **no single correct method** for handling missing data.
    
- The strategy depends on:
    
    - dataset size
        
    - domain knowledge
        
    - percentage of missing values
        
    - relationship with other features
        

In this example, we clean the **Ames Housing Dataset** to prepare it for later regression models.

---

# 1. Import Libraries

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

Load the feature description file:

```python
with open('../DATA/Ames_Housing_Feature_Description.txt','r') as f: 
    print(f.read())
```

This file explains **what each variable means**, which is crucial when deciding how to handle missing data.

---

# 2. Load Dataset

```python
df = pd.read_csv("../DATA/Ames_outliers_removed.csv")
df.head()
```

Check dataset structure:

```python
len(df.columns)
df.info()
```

This helps us understand:

- number of features
    
- data types
    
- missing values
    

---

# 3. Removing Unnecessary Columns

```python
df = df.drop('PID',axis=1)
```

Reason:

- `PID` is a **unique identifier**
    
- It contains **no predictive information**
    
- Keeping it may confuse models
    

---

# 4. Observing Missing Data

Check missing values:

```python
df.isnull()
df.isnull().sum()
100 * df.isnull().sum() / len(df)
```

This shows:

- which columns contain missing values
    
- how many missing entries exist
    

---

# 5. Calculate Percentage of Missing Data

Create a helper function:

```python
def percent_missing(df):
    percent_nan = 100 * df.isnull().sum() / len(df)
    percent_nan = percent_nan[percent_nan > 0].sort_values()
    return percent_nan
```

Use the function:

```python
percent_nan = percent_missing(df)
```

Visualize missing data:

```python
sns.barplot(x=percent_nan.index,y=percent_nan)
plt.xticks(rotation=90);
```


---

# 1️⃣ What the semicolon does in Jupyter

In a Jupyter notebook, the **last expression in a cell automatically prints its output**.

Example:

```python
plt.xticks(rotation=90)
```

Jupyter prints the returned value:

```
([tick locations], [Text objects])
```

This looks messy and is **not useful visually**, but it appears because the function returns something.

---

# 2️⃣ Adding `;` suppresses the output

When you write:

```python
plt.xticks(rotation=90);
```

the semicolon tells Jupyter:

> “Don't print the return value.”

So the plot still renders, but **the extra text disappears**.

---

# 3️⃣ Example comparison

### Without `;`

```python
plt.xticks(rotation=90)
```

Output:

```
([0,1,2,3...], [Text(0,0,'Lot Frontage'), ...])
```

---

### With `;`

```python
plt.xticks(rotation=90);
```

Output:

```
(no extra text)
```

Just the plot.

---

# 4️⃣ Important: this is **Jupyter-specific behavior**

In a normal Python script (`.py` file):

```python
plt.xticks(rotation=90)
```

nothing would print anyway.

The semicolon mainly exists for **notebook cleanliness**.

---

# 5️⃣ Why ML notebooks use it everywhere

Many tutorials include:

```python
plt.xticks(rotation=90);
```

because it:

- prevents ugly output
    
- keeps notebooks clean
    
- focuses attention on the plot
    

---

# 6️⃣ Small tip for your data science workflow

You’ll often see plotting code like this:

```python
sns.barplot(x=percent_nan.index, y=percent_nan)
plt.xticks(rotation=90)
plt.title("Percentage of Missing Data")
plt.show()
```

Here `plt.show()` also **prevents unwanted return output**, so the semicolon becomes unnecessary.

---

# 6. Strategy: Drop Rows vs Fill Values

There are two common approaches:

### 1️⃣ Drop Rows

If **very few rows are missing values**, we can simply remove them. 但是你也要看根据变量的含义 到底是drop还是填0填none 还是别的操作 

Pros:

- Simple
    
- No assumptions
    

Cons:

- Lose training data
    

---

### 2️⃣ Fill Missing Values (Imputation)

Instead of deleting rows, we fill missing values using:

- domain knowledge
    
- statistics
    
- other related features
    

---

# 7. Threshold Strategy

We define a rule:

**If < 1% of rows are missing → drop rows**

Example:

```python
percent_nan[percent_nan < 1]
```

This identifies columns where missing data is very small.

---

# 8. Basement Feature Example

Many basement features use **NaN to mean “no basement”**.

So instead of dropping rows, we **replace missing values**.

---

## Numerical Basement Columns

```python
bsmt_num_cols = [
'BsmtFin SF 1',
'BsmtFin SF 2',
'Bsmt Unf SF',
'Total Bsmt SF',
'Bsmt Full Bath',
'Bsmt Half Bath'
]

df[bsmt_num_cols] = df[bsmt_num_cols].fillna(0)
```

Explanation:

If a house has **no basement**, these values should be **0**.

---

## Categorical Basement Columns

```python
bsmt_str_cols = [
'Bsmt Qual',
'Bsmt Cond',
'Bsmt Exposure',
'BsmtFin Type 1',
'BsmtFin Type 2'
]

df[bsmt_str_cols] = df[bsmt_str_cols].fillna('None')
```

Explanation:

- `"None"` means **no basement exists**
    

---

# 9. Dropping Rows with Missing Values

If only a **few rows are missing**, we can remove them.

Example:

```python
df = df.dropna(axis=0,subset=['Electrical','Garage Cars'])
```

Meaning:

Remove rows where **Electrical or Garage Cars is missing**.

---

# 10. Masonry Veneer Example

From the dataset description:

- If `Mas Vnr Type` is NaN → house has **no masonry veneer**
    

So we fill values:

```python
df["Mas Vnr Type"] = df["Mas Vnr Type"].fillna("None")
df["Mas Vnr Area"] = df["Mas Vnr Area"].fillna(0)
```

---

# 12. Dropping Feature Columns

If a feature has **too many missing values**, we may remove the entire column.

Example:

```python
df = df.drop(['Pool QC','Misc Feature','Alley','Fence'],axis=1)
```

Reason:

These features have **extremely high missing percentages**.

---

# 13. Fireplace Quality

If `Fireplace Qu` is missing, it usually means:

**no fireplace**

```python
df['Fireplace Qu'] = df['Fireplace Qu'].fillna("None")
```

---

# 14. Imputation Using Other Features

Sometimes missing values can be estimated using **related variables**.

Example:

- `Lot Frontage` = street length connected to property
    
- Houses in the same **Neighborhood** tend to have similar frontage sizes.

因为它俩相关联

---

# 15. Visualizing the Relationship

```python
sns.boxplot(
    x='Lot Frontage',
    y='Neighborhood',
    data=df,
    orient='h'
)
```

This helps confirm the relationship.

---

# 16. Group-Based Imputation

We fill missing `Lot Frontage` values using the **average within each neighborhood**.

```python
df['Lot Frontage'] = df.groupby('Neighborhood')['Lot Frontage'] \
    .transform(lambda val: val.fillna(val.mean()))
```

Explanation:

For each neighborhood:

```
LotFrontage_missing → replaced with neighborhood mean
```

# Super intuitive version (no lambda)

If this still feels abstract, here’s a clearer version:

`means = df.groupby('Neighborhood')['Lot Frontage'].mean()`

Now you have:

A → 90  
B → 60

Then:
```python
df['Lot Frontage'] = df['Lot Frontage'].fillna(  
    df['Neighborhood'].map(means)  
)
```


👉 SAME result, easier to understand.

---

# 17. Final Fill

If any values remain missing: 我觉得这个还是得看少的多不多 要多check 

```python
df['Lot Frontage'] = df['Lot Frontage'].fillna(0)
```

---

# 18. Confirm No Missing Values

```python
percent_nan = percent_missing(df)
percent_nan
```

Now:

```
No missing data remains
```

---

# 19. Save Clean Dataset

```python
df.to_csv("../DATA/Ames_NO_Missing_Data.csv",index=False)
```

This file will be used for **future modeling steps**.

---

# Key Concepts

### Missing Data Strategies

|Method|When to Use|
|---|---|
|Drop rows|Very few missing values|
|Fill with 0|Feature represents absence (garage, basement)|
|Fill with category|e.g. `"None"`|
|Drop column|Too many missing values|
|Group-based imputation|Related features exist|

---

# Important Insight

Missing data **does not always mean bad data**.

Sometimes:

```
NaN = meaningful information
```

Example:

```
NaN in GarageType → house has no garage
```

Understanding the **domain meaning** is crucial.

---
