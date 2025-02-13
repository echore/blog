---
share: true
---


## Python String Methods

Python's `str` class comes with various built-in methods to manipulate strings. Here are some common examples:

```python
mystring = 'hello'
print(mystring.capitalize())  # Capitalizes the first letter: 'Hello'
print(mystring.isdigit())     # Checks if the string contains only digits: False
```

To explore all available string methods:

```python
help(str)
```

---

## Working with Text in Pandas

Pandas extends text manipulation capabilities to its Series objects. These methods can process each element in the Series efficiently. Refer to the [official Pandas documentation](https://pandas.pydata.org/docs/user_guide/text.html) for advanced string indexing and regular expressions.

### Applying Text Methods to a Pandas Series

```python
import pandas as pd

names = pd.Series(['andrew', 'bobo', 'claire', 'david', '4'])
print(names.str.capitalize())  # Capitalizes the first letter of each string
print(names.str.isdigit())     # Checks if each element contains only digits
```

### Splitting, Extracting, and Expanding Strings

```python
tech_finance = ['GOOG,APPL,AMZN', 'JPM,BAC,GS']
tickers = pd.Series(tech_finance)

# Splitting strings into lists
print(tickers.str.split(','))

# Extracting the first ticker from each string
print(tickers.str.split(',').str[0])

# Expanding the split strings into multiple columns
print(tickers.str.split(',', expand=True))
```

---

## Cleaning and Editing Strings

Messy string data can often be cleaned using a combination of `str` methods:

```python
messy_names = pd.Series(["andrew  ", "bo;bo", "  claire  "])

# Removing semicolons and extra spaces
cleaned = messy_names.str.replace(";", "").str.strip()
print(cleaned)

# Capitalizing the cleaned strings
final_names = cleaned.str.capitalize()
print(final_names)
```

---

## Using `apply()` for Custom Cleaning Logic

For more complex cleaning tasks, use `apply()` with a custom function:

```python
def cleanup(name):
    name = name.replace(";", "")
    name = name.strip()
    name = name.capitalize()
    return name

cleaned_names = messy_names.apply(cleanup)
print(cleaned_names)
```

---

## Comparing Performance: `.str` vs `apply()` vs `np.vectorize`

When handling large datasets, performance matters. Here's an example using the `timeit` module to measure the execution time of different approaches:

### Setup Code

```python
import pandas as pd
import numpy as np

messy_names = pd.Series(["andrew  ", "bo;bo", "  claire  "])

def cleanup(name):
    name = name.replace(";", "")
    name = name.strip()
    name = name.capitalize()
    return name
```

### Measuring Performance

```python
import timeit

stmt_pandas_str = ''' 
messy_names.str.replace(";", "").str.strip().str.capitalize()
'''

stmt_pandas_apply = '''
messy_names.apply(cleanup)
'''

stmt_pandas_vectorize = '''
np.vectorize(cleanup)(messy_names)
'''

print(timeit.timeit(setup=setup, stmt=stmt_pandas_str, number=10000))
print(timeit.timeit(setup=setup, stmt=stmt_pandas_apply, number=10000))
print(timeit.timeit(setup=setup, stmt=stmt_pandas_vectorize, number=10000))
```

### Key Takeaway

- `.str` methods are convenient for most use cases.
- `apply()` offers flexibility for custom logic but may be slower.
- `np.vectorize()` provides a balance of performance and flexibility, often outperforming `apply()`.
