---
share: true
---

## 🧪 Plot 1: Scatter Plot – Age vs Employment Days

**Goal**: Show relationship between age and employment duration for people who are employed.

✅ Transform both `DAYS_BIRTH` and `DAYS_EMPLOYED` to positive values  
✅ Filter out currently unemployed individuals

```python
df1 = df[df['DAYS_EMPLOYED'] < 0]
df1['DAYS_EMPLOYED'] = df1['DAYS_EMPLOYED'] * -1
df1['DAYS_BIRTH'] = df1['DAYS_BIRTH'] * -1

plt.figure(figsize=(12,8))
sns.scatterplot(
    x='DAYS_BIRTH', 
    y='DAYS_EMPLOYED', 
    data=df1, 
    s=5, 
    linewidth=0, 
    alpha=0.1
)
```

---

## 📈 Plot 2: Distribution of Age (Histogram)

**Goal**: Show distribution of applicant age in years.

```python
df1['Age in Years'] = df1['DAYS_BIRTH'] / 365

plt.figure(figsize=(12,8))
sns.histplot(data=df1, x='Age in Years', bins=50, color='pink')
plt.ylim(0, 14000)
plt.show()
```

---

## 📦 Plot 3: Boxplot – Family Status vs Income (Bottom 50% only)

**Goal**: Show income distribution by family status for the bottom half of income earners.

### Option 1: Using `nsmallest` (based on values)

```python
bottom_half_df = df.nsmallest(int(len(df)/2), columns='AMT_INCOME_TOTAL')

sns.boxplot(
    x='NAME_FAMILY_STATUS', 
    y='AMT_INCOME_TOTAL', 
    data=bottom_half_df, 
    hue='FLAG_OWN_REALTY'
)
plt.legend(bbox_to_anchor=(1.2,1))
```

### Option 2: Using `sort_values().tail()` (based on position)

```python
df_sorted = df.sort_values(by='AMT_INCOME_TOTAL', ascending=False)
bottom_half = df_sorted.tail(len(df) // 2)

plt.figure(figsize=(12,6))
sns.boxplot(
    x='NAME_FAMILY_STATUS', 
    y='AMT_INCOME_TOTAL', 
    data=bottom_half, 
    hue='FLAG_OWN_REALTY'
)
plt.legend(bbox_to_anchor=(1.1,1))
```

🧠 **Note**: These two methods may give slightly different results due to how they handle duplicates and sorting logic.

---

## 🔥 Plot 4: Heatmap – Feature Correlation

**Goal**: Show correlation between numeric features in the dataset.

```python
# Drop FLAG_MOBIL since it has no variance
df_corr = df.drop('FLAG_MOBIL', axis=1)

sns.heatmap(df_corr.corr(numeric_only=True), cmap='viridis')
```

---


For plot 3 I originally use option2 and got different results, here are the explanations:

### 🧪 1. Your first method: `nsmallest(...)`

```python
bottom_half_df = df.nsmallest(int(len(df)/2), columns='AMT_INCOME_TOTAL')
```

- This grabs **exactly** the smallest half of values in `'AMT_INCOME_TOTAL'` — it's _value-based_ selection.
    
- It's **guaranteed** to return the smallest 50% based on actual numeric values, regardless of duplicates or distribution.
    

---

### 🧪 2. Your second method: `sort_values(...).tail(...)`

```python
df_sorted = df.sort_values(by='AMT_INCOME_TOTAL', ascending=False)
half_n = len(df_sorted) // 2
bottom_half = df_sorted.tail(half_n)
```

- Here, you're sorting from **largest to smallest**, and then taking the **last half**.
    
- This also seems like you're getting the smallest 50%, but this is **position-based**. If there are a lot of **duplicate values near the middle**, this may include or exclude some rows differently from `nsmallest`.
    

---

### 🔍 So what's the real difference?

They differ when:

- There are **many duplicate values around the middle**, or
    
- The number of rows isn’t perfectly divisible by 2, or
    
- `nsmallest()` doesn't preserve order like `tail()` after sorting might.
    

Even though they feel equivalent, `nsmallest()` and `sort + tail()` are subtly different in behavior.

---

### ✅ Recommendation:

If you want the **most reliable way** to get the bottom 50% **based on values**, use:

```python
df.nsmallest(len(df) // 2, columns='AMT_INCOME_TOTAL')
```

If you’re ever unsure, you can compare both sets:

```python
set1 = set(bottom_half_df.index)
set2 = set(bottom_half.index)
print("Difference in index sets:", set1.symmetric_difference(set2))
```

That’ll show you the exact rows that differ.

