---
share: true
---
## 🔥 `.apply()` Method

### ✅ What it does:

- Used to apply a function to a DataFrame column.
- Works with both custom functions and lambda expressions.
- Can process multiple columns together.

### 📌 Examples:

#### **Apply with a function**

```python
def last_four(num):
    return str(num)[-4:] #str: to transform CC Number from int to str,then can be sliced.

df['last_four'] = df['CC Number'].apply(last_four)
```

```python
df['total_bill'].mean()
def yelp(price):
    if price < 10:
        return "$"
    elif 10 <= price < 30:
        return "$$"
    else:
        return "$$$"
df['Expensive'] = df['total_bill'].apply(yelp)
```
Like I can create a customize function and apply it into dataframe.
#### **Apply with [[Lambda|Lambda]]**

```python
df['total_bill'].apply(lambda bill: bill * 0.18)
```

#### **Apply with Multiple Columns**

```python
def quality(total_bill, tip):
    return "Generous" if tip / total_bill > 0.25 else "Other"

df['Tip Quality'] = df[['total_bill', 'tip']].apply(lambda df: quality(df['total_bill'], df['tip']), axis=1)
```

### ✅ **Breaking it Down**

1. **`df[['total_bill', 'tip']]`**
    
    - Selects two columns: `total_bill` and `tip` from the DataFrame.
    - This creates a **subset** of the DataFrame with only these two columns.
2. **`.apply(lambda df: quality(df['total_bill'], df['tip']), axis=1)`**
    
    - `lambda df: quality(df['total_bill'], df['tip'])`
        - Defines an **anonymous function** (`lambda` function) that takes each **row** (`df`).
        - Extracts `total_bill` and `tip` from the row.
        - Passes them into the `quality()` function.
    - `axis=1`
        - Ensures the function is applied **row-wise** (each row is treated as `df`).
        - This means the function is applied **once per row**, using that row’s `total_bill` and `tip`.
3. **`df['Tip Quality'] = ...`**
    
    - Saves the result into a new column named `"Tip Quality"`.

1. **`.apply()` should be used row-wise for multiple columns**
    
    - The `apply()` function by default applies the function to each column, **not rows**.
    - Since `quality()` needs both `total_bill` and `tip` from the same row, you must use `.apply()` **along `axis=1`**.
#### **Using `np.vectorize()` for faster execution**

```python
import numpy as np
df['Tip Quality'] = np.vectorize(quality)(df['total_bill'], df['tip'])
```

✅ **Tip:** `np.vectorize()` is significantly faster than `.apply()` when applying functions to multiple columns.
`.apply()` runs **row by row**, making it slower for large datasets
`np.vectorize()` applies the function directly to the entire column, making it much faster!

---

## 📊 `.describe()` – Statistical Summary

```python
df.describe()  # General statistics
df.describe().transpose()  # Transposed for readability
```

🚀 **Use case:** Quickly summarize numerical columns.

---

## 🔀 `.sort_values()` – Sorting Data

```python
df.sort_values('tip')  # Sort by a single column
df.sort_values(['tip', 'size'])  # Sort by multiple columns
```

📌 **Tip:** Use `sort_values()` to reorder your DataFrame.

---

## 📈 `.corr()` – Correlation Matrix

```python
df.corr()
df[['total_bill', 'tip']].corr()
```

🔍 **Insight:** Shows relationships between numerical columns.
#### What is Correlation?

- Correlation measures the **strength** and **direction** of the relationship between two numerical variables.
- The value of correlation **ranges from -1 to 1**:
    - **+1** → Perfect positive correlation (as one increases, the other increases).
    - **0** → No correlation (variables are independent).
    - **-1** → Perfect negative correlation (as one increases, the other decreases).

---

## 🏆 `.idxmin()` and `.idxmax()` – Find Min/Max Index

```python
df['total_bill'].idxmax()  # Index of the highest bill
df['total_bill'].idxmin()  # Index of the lowest bill
df.iloc[df['total_bill'].idxmax()]  # Retrieve row with max value
```

🔍 **Insight:** Use these methods to find the row index of extreme values.

---

## 🔢 `.value_counts()` – Count Unique Values

```python
df['sex'].value_counts()
```

📌 **Use case:** Count occurrences of categorical values.

---

## 🔍 `.unique()` and `.nunique()` – Find Unique Values

```python
df['size'].unique()  # List of unique values
df['size'].nunique()  # Count of unique values
```

📌 **Use case:** Check how many unique categories exist in a column.

---

## 🔄 `.replace()` – Replace Values

```python
df['Tip Quality'].replace(to_replace='Other', value='Ok', inplace=True)
```

🚀 **Use case:** Quickly replace specific values in a DataFrame. Just a few items

---

## 🎭 `.map()` – Value Mapping

```python
my_map = {'Dinner': 'D', 'Lunch': 'L'}
df['time'].map(my_map)
```

📌 **Use case:** Convert categorical values into abbreviated forms.  For many items

---

## 🗂 `.duplicated()` & `.drop_duplicates()` – Handle Duplicates

```python
df.duplicated()  # Returns True for duplicate rows
df.drop_duplicates(inplace=True)  # Remove duplicate rows
```

📌 **Use case:** Clean dataset by removing duplicate entries.
It returns a **Boolean Series**, where:
- `False` means the row is **not** a duplicate (i.e., it appears for the first time).
- `True` means the row is a **duplicate** (i.e., it has appeared before in the DataFrame).

---

## 📍 `.between()` – Range Filtering

```python
df[df['total_bill'].between(10, 20, inclusive=True)]
```

📌 **Use case:** Filter rows within a numerical range.

---

## 🎲 `.sample()` – Random Sampling

```python
df.sample(5)  # Get 5 random rows
df.sample(frac=0.1)  # Get 10% of the dataset
```

📌 **Use case:** Useful for testing or creating smaller datasets.

---

## 🔝 `.nlargest()` & `.nsmallest()` – Get Top/Bottom N Values

```python
df.nlargest(10, 'tip')  # Top 10 highest tips
df.nsmallest(5, 'total_bill')  # 5 smallest total bills
```

📌 **Use case:** Identify extreme values in your dataset.

---

### 🎯 **Final Notes**

- Pandas has many built-in methods; this is just a small selection.
- For a deep dive, check the [Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/index.html).
- Experiment with these methods to get comfortable using them in real-world data analysis! 🚀
