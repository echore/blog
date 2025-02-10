---
share: true
---

## Groupby Method Basics

### Creating a Groupby Object

To use the `groupby` method, you first create a `groupby` object and then apply an aggregation method:

```python
df.groupby('model_year')
```

### Common Aggregation Methods

Once the object is grouped, here are common methods to aggregate the data:

- `mean()`: Compute the mean of groups
- `sum()`: Compute the sum of group values
- `size()`: Compute group sizes
- `count()`: Count non-NA values in groups
- `std()`: Compute the standard deviation of groups
- `var()`: Compute the variance of groups
- `sem()`: Compute the standard error of the mean
- `describe()`: Generate descriptive statistics
- `first()`: Return the first group value
- `last()`: Return the last group value
- `nth(n)`: Return the nth value (or subset if n is a list)
- `min()`: Compute the minimum of group values
- `max()`: Compute the maximum of group values

[Full list of aggregation methods in the pandas documentation](https://pandas.pydata.org/docs/reference/groupby.html)

---

### Aggregating Data

Example of applying aggregation methods:

```python
df.groupby('model_year').mean(numeric_only=True)
```

#### Example Output

- **`model_year`** becomes the index:

```python
avg_year = df.groupby('model_year').mean(numeric_only=True)
avg_year.index
avg_year.columns
avg_year['mpg']
df.groupby('model_year').mean()['mpg']
```

To view descriptive statistics:

```python
df.groupby('model_year').describe()
df.groupby('model_year').describe().transpose()
```

---

## Grouping by Multiple Columns

### Example: Average `mpg` per `model_year` and `cylinders`

```python
df.groupby(['model_year', 'cylinders']).mean()
```

### Understanding MultiIndex

After grouping by multiple columns, pandas uses a **MultiIndex**:

```python
year_cyl = df.groupby(['model_year', 'cylinders']).mean()
year_cyl.index
year_cyl.index.levels
year_cyl.index.names
```

---

## Indexing and Filtering with MultiIndex

### Selecting Data

- Based on **outer index**:
    
    ```python
    year_cyl.loc[70]
    year_cyl.loc[[70, 72]]
    ```
    
- Based on **specific row**:
    
    ```python
    year_cyl.loc[(70, 8)]
    ```
    

### Cross-Section (`.xs()`)

Use `.xs()` to filter specific levels of a MultiIndex:

```python
year_cyl.xs(key=70, axis=0, level='model_year')
year_cyl.xs(key=4, axis=0, level='cylinders')
```

### Basic Concept of `.xs()`

- `.xs()` stands for "cross-section."
- It is used to extract rows or columns based on the value of a specific level in a MultiIndex DataFrame or Series.
### When to Use `.xs()` vs Other Methods

- `.xs()` is ideal for slicing along a particular level in a MultiIndex.
- For simpler filtering, you might use `.loc[]` or `.query()` instead, but they may not handle MultiIndex as cleanly.

#### Comparison with `.loc[]`

`.loc[]` is more general but less concise for MultiIndex:

`df.loc[('A', slice(None)), :]`  vs.  `df.xs('A', level='Group')`

### Common Pitfalls

1. **Not Using `level`:** If you don’t specify the `level`, pandas may not know which level of the index to slice on.
2. **Dropping Levels:** By default, `.xs()` drops the sliced level. Use `drop_level=False` if you want to retain it.

---

### Why Is `.xs()` Powerful?

- It simplifies handling **hierarchical data** without requiring manual restructuring.
- Useful for slicing specific subsets of large datasets.

---

### Syntax

`DataFrame.xs(key, axis=0, level=None, drop_level=True)`

#### Parameters:

1. **`key`**:
    - The label of the level you want to extract.
2. **`axis`**:
    - Whether you are slicing rows (`axis=0`, default) or columns (`axis=1`).
3. **`level`**:
    - The name or index of the level in the MultiIndex you want to select.
4. **`drop_level`**:
    - Whether to drop the level you are slicing from the resulting DataFrame/Series (`True` by default).
---

### Filtering Before Grouping

Keep in mind, its usually much easier to filter out values **before** running a groupby() call, so you should attempt to filter out any values/categories you don't want to use. For example, its much easier to remove **4** cylinder cars before the groupby() call, very difficult to this sort of thing after a group by.

```python
df[df['cylinders'].isin([6,8])].groupby(['model_year','cylinders']).mean(numeric_only=True)
```

---

## Advanced MultiIndex Operations

### Swapping Levels

Swap levels of a MultiIndex:

```python
year_cyl.swaplevel().head()
```

The `swaplevel()` method in pandas is a powerful tool for rearranging the levels of a **MultiIndex** in DataFrames or Series. This function allows you to swap two specified levels, which can be particularly useful when you need to reorganize your data for analysis or visualization.

---

#### Understanding `swaplevel()`

- **Purpose**: To interchange two levels in a MultiIndex, either in the row index or the column index.
- **Common Use Cases**:
    - Reordering hierarchical levels to facilitate data selection or aggregation.
    - Preparing data for operations that require a specific level order.

### Sorting MultiIndex

Sort the MultiIndex based on a specific level:

```python
year_cyl.sort_index(level='model_year', ascending=False)
year_cyl.sort_index(level='cylinders', ascending=False)
```

---

## Advanced Aggregation with `agg()`

The `agg()` method in pandas is a versatile function that allows you to perform one or more aggregation operations across a DataFrame or Series. It's particularly useful for summarizing data, especially after grouping operations.

---

#### Understanding `agg()`

- **Purpose**: To apply one or more aggregation functions over a specified axis (rows or columns) of a DataFrame or Series.
- **Common Use Cases**:
    - Calculating summary statistics like sum, mean, min, max, etc.
    - Applying multiple aggregation functions simultaneously.
    - Aggregating data after grouping operations.

### Using `agg()` on a DataFrame

You can apply multiple aggregation methods to columns:

```python
df.agg(['median', 'mean'])
df.agg(['sum', 'mean'])[['mpg', 'weight']]
```

### Custom Aggregation by Column

Pass a dictionary to specify aggregation methods for specific columns:

```python
df.agg({'mpg': ['median', 'mean'], 'weight': ['mean', 'std']})
```

### Combining `agg()` with Groupby

```python
df.groupby('model_year').agg({
    'mpg': ['median', 'mean'],
    'weight': ['mean', 'std']
})
```

---

### Useful Links for Reference

- [Groupby Documentation](https://pandas.pydata.org/docs/reference/groupby.html)
- [MultiIndex Advanced Operations](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html)

---
