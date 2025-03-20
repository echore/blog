---
share: true
---


## 📦 Boxplot (Distribution with Quartiles & Outliers)

A **boxplot** displays the distribution of numerical data based on:

- **Quartiles (25%, 50%, 75%)**
- **Interquartile Range (IQR)**
- **Outliers** (points outside 1.5 × IQR)

```python
plt.figure(figsize=(12,6))
sns.boxplot(x='parental level of education', y='math score', data=df)
```

### 🏷️ Adding `hue` for Segmentation

```python
plt.figure(figsize=(12,6))
sns.boxplot(x='parental level of education', y='math score', data=df, hue='gender')
```

### 📍 Moving Legend Outside

```python
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
```

### 🎨 Boxplot Styling

#### **Orientation** (Horizontal Boxplot)

Switch **X** and **Y** for readability:

```python
sns.boxplot(x='math score', y='parental level of education', data=df, orient='h')
```

#### **Width of Boxes**

```python
plt.figure(figsize=(12,6))
sns.boxplot(x='parental level of education', y='math score', data=df, hue='gender', width=0.3)
```

---

## 🎻 Violinplot (KDE + Boxplot Hybrid)

A **violin plot** visualizes the distribution using:

- **Kernel Density Estimation (KDE)**
- **Boxplot elements (optional)**

```python
plt.figure(figsize=(12,6))
sns.violinplot(x='parental level of education', y='math score', data=df)
```

### 🏷️ Adding `hue`

```python
plt.figure(figsize=(12,6))
sns.violinplot(x='parental level of education', y='math score', data=df, hue='gender')
```

### 🎭 Violinplot Parameters

#### **Split Violins for Comparison**

```python
plt.figure(figsize=(12,6))
sns.violinplot(x='parental level of education', y='math score', data=df, hue='gender', split=True)
```

#### **Different Inner Representations**

```python
sns.violinplot(x='parental level of education', y='math score', data=df, inner=None)        # No inner elements
sns.violinplot(x='parental level of education', y='math score', data=df, inner='box')       # Mini boxplot
sns.violinplot(x='parental level of education', y='math score', data=df, inner='quartile')  # Quartiles
sns.violinplot(x='parental level of education', y='math score', data=df, inner='stick')     # Individual datapoints
```

#### **Orientation (Horizontal Violin)**

```python
sns.violinplot(x='math score', y='parental level of education', data=df)
```

#### **Bandwidth Control (Smoothing)**

```python
plt.figure(figsize=(12,6))
sns.violinplot(x='parental level of education', y='math score', data=df, bw=0.1)
```

---

## 🐝 Swarmplot (Scatterplot for Categories)

A **swarmplot** shows individual data points **without overlapping**.

```python
sns.swarmplot(x='math score', data=df)
sns.swarmplot(x='math score', data=df, size=2)
```

### 🏷️ Swarmplot with Categories

```python
sns.swarmplot(x='math score', y='race/ethnicity', data=df, size=3)
sns.swarmplot(x='race/ethnicity', y='math score', data=df, size=3)
```

### 🏷️ Swarmplot with Hue

```python
plt.figure(figsize=(12,6))
sns.swarmplot(x='race/ethnicity', y='math score', data=df, hue='gender')
```

### 🏷️ `dodge=True` for Gender Comparison

```python
plt.figure(figsize=(12,6))
sns.swarmplot(x='race/ethnicity', y='math score', data=df, hue='gender', dodge=True)
```

---

## 📦 **Boxenplot (Letter-Value Plot)**

A **boxenplot** provides a **detailed quantile-based summary** of data distribution.

📜 **Reference Paper:** [Letter-Value Plot](https://vita.had.co.nz/papers/letter-value-plot.html)

```python
sns.boxenplot(x='math score', y='race/ethnicity', data=df)
sns.boxenplot(x='race/ethnicity', y='math score', data=df)
```

### 🏷️ Boxenplot with Hue

```python
plt.figure(figsize=(12,6))
sns.boxenplot(x='race/ethnicity', y='math score', data=df, hue='gender')
```

---

## 🔗 References

- [Move Seaborn Legend Outside](https://stackoverflow.com/questions/30490740/move-legend-outside-figure-in-seaborn-tsplot)
- [Matplotlib Colormap Reference](https://matplotlib.org/3.1.1/gallery/color/colormap_reference.html)
- [Letter-Value Plot Paper](https://vita.had.co.nz/papers/letter-value-plot.html)
