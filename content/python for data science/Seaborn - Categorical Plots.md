---
share: true
---
Categorical plots help visualize data that falls into distinct groups (e.g., countries, companies, education levels). Unlike continuous data, categorical data has no "in-between" values.

## 📥 Imports

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

## 📂 The Data

Load a dataset (e.g., `dm_office_sales.csv`) for analysis:

```python
df = pd.read_csv("dm_office_sales.csv")
df.head()
```

---

## 📈 Countplot (Total Count per Category)

A **countplot** displays the number of occurrences of each category.

```python
plt.figure(figsize=(10,4), dpi=200)
sns.countplot(x='division', data=df)
```

Count of education levels:

```python
plt.figure(figsize=(10,4), dpi=200)
sns.countplot(x='level of education', data=df)
```

### 🏷️ Breakdown within Another Category (`hue`)

```python
plt.figure(figsize=(10,4), dpi=200)
sns.countplot(x='level of education', data=df, hue='training level')
```

📌 **Customize Colors with Matplotlib Colormaps:**  
[List of colormaps](https://matplotlib.org/3.1.1/gallery/color/colormap_reference.html)

```python
sns.countplot(x='level of education', data=df, hue='training level', palette='Set1')
sns.countplot(x='level of education', data=df, hue='training level', palette='Paired')  # Good for distinct jumps
```

---

## 📊 Barplot (Statistical Estimation)

A **barplot** aggregates a numerical feature (e.g., salary) by a categorical variable. By default, it displays the **mean**.

```python
plt.figure(figsize=(10,6), dpi=200)
sns.barplot(x='level of education', y='salary', data=df, estimator=np.mean, ci='sd')  # Mean with standard deviation
```

### 🏢 Grouped Barplot with `hue`

```python
plt.figure(figsize=(12,6))
sns.barplot(x='level of education', y='salary', data=df, estimator=np.mean, ci='sd', hue='division')
```

### 📍 Moving Legend Outside the Plot

```python
plt.figure(figsize=(12,6), dpi=100)
sns.barplot(x='level of education', y='salary', data=df, estimator=np.mean, ci='sd', hue='division')
plt.legend(bbox_to_anchor=(1.05, 1))  # Moves legend outside
```

---

## 🔗 References

- [Matplotlib Colormap Reference](https://matplotlib.org/3.1.1/gallery/color/colormap_reference.html)
- [Seaborn Barplot Black Bar Explanation](https://stackoverflow.com/questions/58362473/what-does-black-lines-on-a-seaborn-barplot-mean)
- [Move Seaborn Legend Outside](https://stackoverflow.com/questions/30490740/move-legend-outside-figure-in-seaborn-tsplot)
