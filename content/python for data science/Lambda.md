---
share: true
---

## 🏷️ **Understanding `lambda` Functions in Python**

A **lambda function** is a small **anonymous function** (i.e., a function without a name) that is typically used for short, simple operations. It is also called a **"lambda expression"**.

---

### 🎯 **Basic Syntax**

```python
lambda arguments: expression
```

- `lambda` is the keyword.
- `arguments` are input values, similar to parameters in a normal function.
- `expression` is the operation that will be performed and returned.

👉 **Example (Basic Addition)**

```python
add = lambda x, y: x + y
print(add(2, 3))  # Output: 5
```

📌 **How does it work?**

- `lambda x, y: x + y` → Defines a function that takes `x` and `y` as arguments and returns their sum.
- `add(2, 3)` → Calls the lambda function with arguments `2` and `3`.

---

## 🔥 **Why Use Lambda Functions?**

- **Concise & Readable**: They are one-liners.
- **Used Inside Other Functions**: Often used when you need a quick function inside another function.
- **No Need for `def`**: Saves time when defining small functions.

---

## ⚡ **Examples & Use Cases**

### ✅ **1. Using `lambda` in `map()`**

📌 `map()` applies a function to each item in an iterable.

```python
nums = [1, 2, 3, 4]
squared = list(map(lambda x: x ** 2, nums))
print(squared)  # Output: [1, 4, 9, 16]
```

Equivalent with `def`:

```python
def square(x):
    return x ** 2

squared = list(map(square, nums))
```

---

### ✅ **2. Using `lambda` in `filter()`**

📌 `filter()` keeps values that return `True`.

```python
nums = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)  # Output: [2, 4, 6]
```

Equivalent with `def`:

```python
def is_even(x):
    return x % 2 == 0

evens = list(filter(is_even, nums))
```

---

### ✅ **3. Using `lambda` in `sorted()`**

📌 Custom sorting with `lambda`

```python
students = [('Alice', 25), ('Bob', 20), ('Charlie', 23)]
sorted_students = sorted(students, key=lambda x: x[1])
print(sorted_students)  
# Output: [('Bob', 20), ('Charlie', 23), ('Alice', 25)]
```

🔍 **Explanation:**

- `key=lambda x: x[1]` → Sorts by the **second element** (age).

---

### ✅ **4. Using `lambda` in `pandas`**

📌 Applying operations on DataFrame columns

```python
import pandas as pd

df = pd.DataFrame({'A': [1, 2, 3, 4]})
df['B'] = df['A'].apply(lambda x: x * 2)
print(df)
```

**Output:**

```
   A  B
0  1  2
1  2  4
2  3  6
3  4  8
```

---

## ⚠️ **When NOT to Use `lambda`**

- If the function logic is complex → Use `def` instead.
- If the function is reusable → Named functions are better.

---

## 🎯 **Key Takeaways**

✅ `lambda` creates small anonymous functions.  
✅ Best used for **short, one-time** operations.  
✅ Commonly used in **`map()`, `filter()`, `sorted()`**, and `pandas`.  
✅ If the function gets complex, use **`def` instead**.

