---
share: true
---

## 📝 Overview

Scatter plots help visualize the relationship between two numerical variables. Seaborn provides various enhancements like color grouping (`hue`), size variation (`size`), and different marker styles (`style`).

## 📌 Loading Data

We'll use **Pandas** to load a dataset.

```python
import pandas as pd
import seaborn as sns

# Load dataset
df = pd.read_csv("dm_office_sales.csv")

# Display basic info
df.head()
df.info()
```

---

## 📈 Basic Scatter Plot

```python
sns.scatterplot(x='salary', y='sales', data=df)
```

### 🔍 Matplotlib Integration

Even though Seaborn builds on Matplotlib, we can still modify figures using `matplotlib.pyplot`:

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df)
plt.show()
```

---

## 🎨 Seaborn Parameters

### 1️⃣ **hue** (Color by Category)

Use `hue` to color points based on a categorical feature:

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, hue='division')

plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, hue='work experience')
```

#### 🎨 Custom Color Palette

You can specify a color palette using Matplotlib colormaps:

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, hue='work experience', palette='viridis')
```

---

### 2️⃣ **size** (Varying Marker Size)

Adjust the size of markers based on another column:

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, size='work experience')
```

🔹 **Uniform marker size:**  
Use `s=` to apply a constant marker size:

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, s=200)
```

🔹 **Customize marker transparency & border:**

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, s=200, linewidth=0, alpha=0.2)
```

---

### 3️⃣ **style** (Different Marker Shapes)

Change marker styles based on a categorical feature:

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, style='level of education')
```

🔹 **Combine `hue` and `style` for better distinction**:

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, style='level of education', hue='level of education', s=100)
```

🔹 **Customize markers manually**:

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, style='level of education', markers=['*', '+', 'o'])
```

---

## 📤 Exporting a Seaborn Figure

To save your scatter plot:

```python
plt.figure(figsize=(12,8))
sns.scatterplot(x='salary', y='sales', data=df, style='level of education', hue='level of education', s=100)

# Save figure
plt.savefig('example_scatter.jpg')
```



