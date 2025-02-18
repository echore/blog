---
share: true
---

Pivoting data can help clarify relationships and connections by restructuring how information is displayed. This is especially useful for **data analysis, visualization, and exploration**.

> 🔗 **Full documentation on pivot methods:** [Pandas User Guide - Reshaping](https://pandas.pydata.org/docs/user_guide/reshaping.html)

## 📌 Data Import

```python
import numpy as np
import pandas as pd

df = pd.read_csv('Sales_Funnel_CRM.csv')
df.head()
```

---

## 🔄 `pivot()` Method

The `pivot()` method reshapes data based on column values and reassignment of the index. **It does not perform aggregation**, so it requires a unique index for each combination of values.

### **❓ When to use `pivot()`**

Before using `pivot()`, ask yourself: ✅ What question are you trying to answer?  
✅ What should the transformed DataFrame look like?  
✅ Do you need all the original columns?

---

### **Example: How many licenses of each product did Google purchase?**

```python
# Take a subset to avoid duplicate row errors
licenses = df[['Company', 'Product', 'Licenses']]
licenses.head()

# Apply pivot
pd.pivot(data=licenses, index='Company', columns='Product', values='Licenses')
```

---

## 🛠️ `pivot_table()` Method

The `pivot_table()` method is similar to `pivot()` but allows for **aggregation functions** to be applied.

### **Basic Example: Sum by Company**

```python
pd.pivot_table(df, index="Company", aggfunc='sum')
```

🔹 **Selecting Specific Columns**

```python
# Option 1: Selecting columns after pivoting
pd.pivot_table(df, index="Company", aggfunc='sum')[['Licenses', 'Sale Price']]

# Option 2: Specifying columns before pivoting
pd.pivot_table(df, index="Company", aggfunc='sum', values=['Licenses', 'Sale Price'])
```

🔹 **Alternative Using `groupby()`**

```python
df.groupby('Company').sum()[['Licenses', 'Sale Price']]
```

---

### **🔹 Using Multiple Index Levels**

```python
pd.pivot_table(df, index=["Account Manager", "Contact"], values=['Sale Price'], aggfunc='sum')
```

🔹 **Adding Columns for Further Segmentation**

```python
pd.pivot_table(df, index=["Account Manager", "Contact"], values=["Sale Price"], columns=["Product"], aggfunc=np.sum)
```

🔹 **Filling Missing Values with `fill_value=0`**

```python
pd.pivot_table(df, index=["Account Manager", "Contact"], values=["Sale Price"], 
               columns=["Product"], aggfunc=np.sum, fill_value=0)
```

---

### **📌 Multiple Aggregation Functions**

```python
pd.pivot_table(df, index=["Account Manager", "Contact"], values=["Sale Price"], columns=["Product"],
               aggfunc=[np.sum, np.mean], fill_value=0)
```

---

### **📌 Pivoting with Multiple Columns**

```python
pd.pivot_table(df, index=["Account Manager", "Contact"], values=["Sale Price", "Licenses"], columns=["Product"],
               aggfunc=[np.sum], fill_value=0)
```

---

### **📌 Pivoting with Multiple Indexes**

```python
pd.pivot_table(df, index=["Account Manager", "Contact", "Product"], values=["Sale Price", "Licenses"],
               aggfunc=[np.sum], fill_value=0)
```

---

### **📌 Adding a Grand Total (`margins=True`)**

```python
pd.pivot_table(df, index=["Account Manager", "Contact", "Product"], values=["Sale Price", "Licenses"],
               aggfunc=[np.sum], fill_value=0, margins=True)
```

or

```python
pd.pivot_table(df, index=["Account Manager", "Status"], values=["Sale Price"],
               aggfunc=[np.sum], fill_value=0, margins=True)
```

---

## 🎯 **Key Takeaways**

✔ **Use `pivot()`** when you need to restructure data without aggregation.  
✔ **Use `pivot_table()`** when aggregation (e.g., `sum`, `mean`) is required.  
✔ **Define your question first** to avoid confusion with index, columns, and values.  
✔ **Use `fill_value=0`** to handle missing values.  
✔ **Use `margins=True`** to get totals.
