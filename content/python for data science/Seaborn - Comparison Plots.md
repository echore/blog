---
share: true
---

## 📊 Comparison Plots with `pairplot()` and `jointplot()`

_Use these plots to explore relationships between multiple variables in a dataset, especially during EDA (Exploratory Data Analysis)._

---

### 🔍 Exploring Two Variables with `jointplot()`

```python
sns.jointplot(x='math score', y='reading score', data=df)
```

> 🔹 **Scatterplot with histograms**
> 
> - Shows relationship between math and reading scores.
> - Marginal histograms give insight into individual distributions.

---

```python
sns.jointplot(x='math score', y='reading score', data=df, kind='hex')
```

> 🔹 **Hexbin plot**
> 
> - Replaces scatterplot with a hexagon heatmap.
> - Useful for large datasets where points overlap.

---

```python
sns.jointplot(x='math score', y='reading score', data=df, kind='kde')
```

> 🔹 **KDE plot**
> 
> - Shows smooth contour lines representing data density.
> - Great for visualizing continuous distributions and overall trends.

---

### 🧩 Exploring Multiple Variables with `pairplot()`

```python
sns.pairplot(df)
```

> 🔹 **Basic pairplot**
> 
> - Automatically draws scatterplots for every numeric pair.
> - Diagonal shows univariate histograms (default is KDE if not specified).

---

```python
sns.pairplot(df, hue='gender', palette='viridis')
```

> 🔹 **Colored by category**
> 
> - Uses the `gender` column to color data points.
> - Helps compare variable interactions across groups.

---

```python
sns.pairplot(df, hue='gender', palette='viridis', corner=True)
```

> 🔹 **Lower-triangle only**
> 
> - `corner=True` avoids redundant mirrored plots.
> - More compact and readable.

---

```python
sns.pairplot(df, hue='gender', palette='viridis', diag_kind='hist')
```

> 🔹 **Diagonal uses histograms**
> 
> - Replaces KDE with classic histograms for univariate plots.
> - Better when data isn't smoothly distributed.

---

### ✅ Summary Table

|Function|Use Case|Supports Category Highlight (`hue`)|
|---|---|---|
|`jointplot()`|Visualizing 2 variables|❌ No `hue` support|
|`pairplot()`|Visualizing multiple variables|✅ Yes, with `hue`|

