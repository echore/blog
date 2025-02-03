---
share: true
---
## Key Concept
Filter DataFrames using boolean conditions ("masks") to select specific rows.

## Basic Filtering
### Single Condition

```python
# Create boolean mask
mask = df['total_bill'] > 30

# Apply mask
large_bills = df[mask]
```

**Equivalent shorthand:**
```python
df[df['total_bill'] > 30]
```

### How It Works:
1. `df['total_bill'] > 30` creates boolean Series (True/False values)
2. DataFrame returns rows where mask is True

---

## Multiple Conditions
### AND (&) Operator
```python
# Both conditions must be True
df[(df['total_bill'] > 30) & (df['sex']!='Male')]
```

### OR (|) Operator 
```python
# Either condition can be True
df[(df['day'] == 'Sun') | (df['day'] == 'Sat')]
```


---

## `isin()` Method
Check if values are in a list of options:

```python
# Weekend filter
options = ['Sat','Sun']
df['day'].isin(options)

df[df['day'].isin(['Sat', 'Sun'])]

# Equivalent to:
df[(df['day'] == 'Sat') | (df['day'] == 'Sun')]
```

---

## Why Parentheses Matter
Python operator precedence can cause unexpected behavior:

```python
# ❌ Wrong - evaluates 'Male' & df first!
df[df['total_bill'] > 30 & df['sex'] == 'Male']

# ✅ Correct
df[(df['total_bill'] > 30) & (df['sex'] == 'Male')]
```

---

## Filtering Process
1. **Create Mask:** Generate boolean Series from condition
2. **Apply Mask:** Use `df[mask]` to filter rows
3. **Combine Masks:** Use logical operators (`&`, `|`, `~`) 

---


## Key Takeaways
1. **Boolean Masking:** Core pandas filtering technique
2. **Operator Precedence:** Always use parentheses
3. **`isin()` Efficiency:** Cleaner than multiple OR conditions
4. **Readability:** Break complex filters into multiple lines
