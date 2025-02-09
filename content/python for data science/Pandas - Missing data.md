---
share: true
---

## Representations of Missing Data

Pandas uses the following to represent missing data:

1. **`np.nan`**: For float data.
2. **`None`**: For object-dtype data.
3. **`pd.NaT`**: For datetime-like data.
4. **`pd.NA`**: A new scalar value introduced for consistent representation across all data types.

### Example

```python
import numpy as np
import pandas as pd

print(np.nan)   # Float missing value
print(pd.NA)    # General missing value
print(pd.NaT)   # Datetime missing value
```

---

## Important Notes on Comparisons

- Comparisons with missing values can lead to unexpected results:
    - `np.nan == np.nan` → `False`
    - `np.nan in [np.nan]` → `True`
    - `pd.NA == pd.NA` → `False`
- This happens because missing values are considered "unknown," so equality cannot be determined.

**Further Reading:**

- [Towards Data Science: Navigating NaNs](https://towardsdatascience.com/navigating-the-hell-of-nans-in-python-71b12558895b)
- [StackOverflow: NaN Comparisons](https://stackoverflow.com/questions/20320022/why-in-numpy-nan-nan-is-false-while-nan-in-nan-is-true)

---

## Example Dataset

Imagine a dataset of people's ratings of actors before and after watching a movie, but with some missing data:

```python
df = pd.read_csv('movie_scores.csv')
print(df)
```

---

## Identifying Missing Values

- **`isnull()`**: Detects missing values.
- **`notnull()`**: Detects non-missing values.

### Examples

```python
# Check for missing values
df.isnull()

# Select rows where 'first_name' is not null
df[df['first_name'].notnull()]

# Filter rows with specific conditions
df[(df['pre_movie_score'].isnull()) & (df['sex'].notnull())]
```

---

## Dropping Missing Data

- **`dropna()`**: Removes rows or columns with missing data.

### Options

- **`thresh`**: Minimum non-NA values required to retain the row/column.
- **`axis`**: Drop rows (`axis=0`) or columns (`axis=1`).

### Examples

```python
# Drop rows with any missing values
df.dropna()

# Drop columns with less than 4 non-NA values
df.dropna(thresh=4, axis=1)
```

---

## Filling Missing Data

- **`fillna()`**: Replace missing values with a specific value or computation.

### Examples

```python
# Fill missing values with a string
df.fillna("NEW VALUE!")

# Fill a specific column with a default value
df['first_name'].fillna("Empty", inplace=True)

# Fill with the column mean
df['pre_movie_score'].fillna(df['pre_movie_score'].mean(), inplace=True)

# Fill all numeric columns with their mean
df.fillna(df.mean(), inplace=True)
```

---

## Interpolation

Interpolation is a method of estimating missing values based on existing data.

- **Default method**: Linear interpolation.
- **Other methods**: `spline`, `polynomial`, etc.

### Example

```python
# Create a sample series
airline_tix = {'first': 100, 'business': np.nan, 'economy-plus': 50, 'economy': 30}
ser = pd.Series(airline_tix)

# Linear interpolation
ser.interpolate()

# Spline interpolation
ser.interpolate(method='spline', order=2)
```

**Docs**: [Pandas Interpolate Documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.interpolate.html)

---

## Summary

1. Identify missing data using `isnull()` and `notnull()`.
2. Drop rows or columns using `dropna()`.
3. Fill missing values with default values or computed statistics using `fillna()`.
4. Use interpolation to estimate missing values carefully.

