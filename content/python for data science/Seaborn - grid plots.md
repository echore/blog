---
share: true
---

## 🎯 catplot
base plot 

```python
# Kind Options: "point", "bar", "strip", "swarm", "box", "violin", "boxen"

# Basic boxplot by gender
sns.catplot(x='gender', y='math score', data=df, kind='box')

# Add row = lunch (standard vs free/reduced)
sns.catplot(x='gender', y='math score', data=df, kind='box', row='lunch')

# Add column = test prep course (completed vs none)
sns.catplot(x='gender', y='math score', data=df, kind='box', row='lunch', col='test preparation course')
```

📝 **Use Case**: Ideal when comparing how different categories (like gender, lunch, test prep) impact scores.

---

## 🔁 PairGrid

> A customizable version of `pairplot` for examining relationships between **all numerical features**

```python
# Simple layout: upper = scatter, diag = kde, lower = kde (in red)
g = sns.PairGrid(df)
g = g.map_upper(sns.scatterplot)
g = g.map_diag(sns.kdeplot, lw=2)
g = g.map_lower(sns.kdeplot, color="red")

```

📌 **Note**: If you see a warning about `marker` in kde plots, it's safe to ignore — kde doesn't use markers.

---

## 🗂️ FacetGrid

> Create a grid of plots conditioned on **categorical variables**

```python
# Create grid layout: columns by gender, rows by lunch
g = sns.FacetGrid(data=df, col='gender', row='lunch')

# Map a scatter plot to each subplot
g = g.map(plt.scatter, "math score", "reading score", edgecolor="w")

# Add legend
g.add_legend()

# Adjust spacing between plots
plt.subplots_adjust(hspace=0.4, wspace=1)
```

🔍 **Use Case**: Perfect for comparing bivariate relationships (like math vs reading scores) across different subgroups.


## 🧩 Why use Grid Plots?

Because they help you **compare things side by side**.

---

### ✅ Imagine this:

You want to see:

- Do **boys and girls** score differently?
- Does **lunch type** affect scores?
- What happens if they did a **prep course**?

**One plot** can’t show all of that.  
But **grid plots** split the data into small groups and show **many small plots** — so you can compare **quickly and clearly**.

---

### 🧪 What each grid does:

|Type|Use for...|Looks like|
|---|---|---|
|`catplot`|Compare **groups**|Boxplots per gender/lunch/prep|
|`FacetGrid`|Show **many scatter plots** split by category|One plot per group|
|`PairGrid`|Show how **numbers** relate (math vs reading, etc.)|A big grid of scatter and curves|

---

### 🥪 Analogy:

Grid plots are like a **sandwich tray**.

Each small sandwich (plot) shows part of the full picture.  
Instead of one big messy sandwich, you get **bite-sized**, easy-to-read plots.
