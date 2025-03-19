---
share: true
---

## 🔹 Overview

There are multiple ways to display the distribution of a feature. This note covers three key methods:

1. **Rugplot** – Simple but not ideal for large datasets.
2. **Histograms** – Shows distribution using bins.
3. **Kernel Density Estimation (KDE)** – Smooths the distribution.

---

## 🗂 Data Source

- Dataset used: `dm_office_sales.csv`
- Alternative: Generate random data using `numpy` (`np.random.randint()` or `np.random.normal()`).

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("dm_office_sales.csv")
df.head()
df.info()
```

---

## 📌 1. Rugplot 🏷️

A rugplot places a small tick on the x-axis for each data point.

```python
sns.rugplot(x='salary', data=df)
sns.rugplot(x='salary', data=df, height=0.5)
```

🔹 **Limitations**: Not useful for large datasets as it becomes cluttered.

---

## 📌 2. Histograms 📊

A **histogram** groups data into bins and counts occurrences.

```python
sns.displot(data=df, x='salary', kde=True)  # Histogram + KDE
sns.displot(data=df, x='salary')  # Only histogram
sns.histplot(data=df, x='salary')  # Alternative method
```

### 🎛 Adjusting Bin Size

- **More bins** = more granularity.
- **Fewer bins** = smoother distribution.

```python
sns.histplot(data=df, x='salary', bins=10)
sns.histplot(data=df, x='salary', bins=100)
```

---

## 🎨 Styling Histograms

### 🌫️ Grid Styles

Change the background style:

```python
sns.set(style='darkgrid')  # Options: darkgrid, whitegrid, dark, white, ticks
sns.histplot(data=df, x='salary', bins=100)
```

### 🎨 Custom Styling

You can modify colors, edge styles, and linewidth.

```python
sns.displot(data=df, x='salary', bins=20, kde=False,
            color='red', edgecolor='black', lw=4, ls='--')
```

---

## 📌 3. Kernel Density Estimation (KDE) 📈

KDE provides a smoothed estimate of the probability density function (PDF).

```python
sns.kdeplot(data=df, x='salary')
```

### 🔹 Example with Random Data

```python
np.random.seed(42)
sample_ages = np.random.randint(0, 100, 200)
sample_ages = pd.DataFrame(sample_ages, columns=["age"])

sns.kdeplot(data=sample_ages, x='age')
```

### ✂ Cutting Off KDE (If Data Has Limits)

To prevent KDE from estimating outside known values (e.g., negative ages):

```python
sns.kdeplot(data=sample_ages, x='age', clip=[0, 100])
```

---

## 📏 Bandwidth Adjustment

- Bandwidth controls the smoothness of the KDE.
- Smaller values = more sensitivity (narrow peaks).
- Larger values = smoother curve.

```python
sns.kdeplot(data=sample_ages, x='age', bw_adjust=0.1)
sns.kdeplot(data=sample_ages, x='age', bw_adjust=0.5)
sns.kdeplot(data=sample_ages, x='age', bw_adjust=1)
```

---

## 🌈 Advanced Styling

Enable shading and custom colors:

```python
sns.kdeplot(data=sample_ages, x='age', bw_adjust=0.5, shade=True, color='red')
```

---

## 📌 4. 2D KDE Plots 🌍

Compare two continuous features using a **2D KDE plot**.

```python
random_data = pd.DataFrame(np.random.normal(0,1,size=(100,2)), columns=['x', 'y'])
sns.kdeplot(data=random_data, x='x', y='y')
```

---

## 🏆 Summary

|Plot Type|Description|Best Use Case|
|---|---|---|
|Rugplot|Marks each data point on x-axis|Small datasets|
|Histogram|Groups data into bins|General distribution analysis|
|KDE|Smooth distribution curve|Understanding probability density|
