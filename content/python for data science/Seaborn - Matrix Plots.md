---
share: true
---

## 🔥 Heatmap

### Step 1: Set index to country names

```python
df = df.set_index('Countries')
```

### Step 2: Initial heatmap (includes all columns, including life expectancy)

```python
sns.heatmap(df)
```

### Step 3: Drop `Life expectancy` column for clearer numerical focus

```python
rates = df.drop('Life expectancy', axis=1)
```

### Step 4: Adjust visual details

```python
sns.heatmap(rates)  # Default
sns.heatmap(rates, linewidth=0.5)  # Add cell borders
sns.heatmap(rates, linewidth=0.5, annot=True)  # Show numbers
```

### Step 5: Customize with color palettes

```python
sns.heatmap(rates, linewidth=0.5, annot=True, cmap='viridis')
```

### Step 6: Center colorbar on a specific value

```python
sns.heatmap(rates, linewidth=0.5, annot=True, cmap='viridis', center=40)  # Center at 40
sns.heatmap(rates, linewidth=0.5, annot=True, cmap='viridis', center=1)   # Center at 1
```

> 🔍 `center` helps highlight deviation from a key value (e.g., population growth rate = 1) but don't recommend using center method, default is fine

---

## 🧬 Clustermap

Use clustermap to **group similar rows/columns** using hierarchical clustering.

```python
sns.clustermap(rates)
```

### Turn off column clustering (for fixed column order):

```python
sns.clustermap(rates, col_cluster=False)
```

### Adjust figure size and colorbar position:

```python
sns.clustermap(
    rates,
    col_cluster=False,
    figsize=(12, 8),
    cbar_pos=(-0.1, .2, .03, .4)  # [left, bottom, width, height]
)
```

### Optional: Clean up row index name

```python
rates.index.set_names('', inplace=True)
```

---

## ✅ Key Takeaways

- `heatmap` is good for visualizing raw matrix data.
    
- `clustermap` is ideal for discovering patterns/groupings.
    
- Use `annot=True` to display actual values.
    
- Use `center` to customize midpoint in colormap (useful for diverging palettes).
    
- Always clean/preprocess your DataFrame before plotting.
    
