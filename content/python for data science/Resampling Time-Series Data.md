---
share: true
---

Resampling in Pandas allows you to **change the frequency of your time-series data**. This is particularly useful when you want to:

- Aggregate data to a lower frequency (e.g., daily to monthly or yearly).
- Upsample data to a higher frequency (e.g., monthly to daily).

It uses a combination of the `resample()` method and an aggregation function (e.g., `mean`, `sum`, `count`) to group and summarize data.

---

### 1. **Basic Syntax**

```python
data.resample(rule).agg(function)
```

- `rule`: A string specifying the new frequency (e.g., `'M'` for monthly, `'A'` for yearly).
- `agg(function)`: An aggregation method like `mean`, `sum`, or `count`.

---

### 2. **Time-Series Offset Aliases**

Common **frequency strings** for resampling:

- `'D'` : Daily
- `'W'` : Weekly
- `'M'` : Month-end
- `'MS'`: Month-start
- `'A'` : Year-end
- `'H'` : Hourly

A full list is available in the [Pandas documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#offset-aliases).

---

### 3. **Example: Resampling in Action**

Let's start with a simple example:

#### Example Data

```python
import pandas as pd
import numpy as np

# Create a sample DataFrame with a datetime index
date_rng = pd.date_range(start='2023-01-01', end='2023-01-10', freq='D')
data = pd.DataFrame(date_rng, columns=['Date'])
data['Sales'] = np.random.randint(100, 500, size=(len(date_rng)))
data = data.set_index('Date')

print(data)
```

Sample Output:

```
            Sales
Date             
2023-01-01   239
2023-01-02   455
2023-01-03   341
2023-01-04   408
2023-01-05   181
2023-01-06   134
2023-01-07   274
2023-01-08   120
2023-01-09   467
2023-01-10   331
```

---

### 4. **Downsampling (Reduce Frequency)**

#### Example: Resample to Weekly Frequency

```python
# Resample to weekly frequency and calculate the sum of sales for each week
weekly_sales = data.resample('W').sum()
print(weekly_sales)
```

Sample Output:

```
            Sales
Date             
2023-01-01   239
2023-01-08  1988
2023-01-15   798
```

In this example:

- The first row (`2023-01-01`) contains only the sales for that day.
- The second row (`2023-01-08`) aggregates sales from `2023-01-02` to `2023-01-08`.

#### Example: Resample to Monthly Frequency

```python
monthly_sales = data.resample('M').mean()
print(monthly_sales)
```

---

### 5. **Upsampling (Increase Frequency)**

Upsampling is used to create higher-frequency data by filling in missing values.

#### Example: Resample to Daily Frequency

```python
# Resample to hourly frequency (Upsample)
hourly_data = data.resample('H').asfreq()
print(hourly_data)
```

By default, the new rows will have `NaN` values for missing data.

#### Fill Missing Values

You can handle missing values during upsampling:

```python
# Forward-fill missing data
hourly_data_filled = data.resample('H').ffill()
print(hourly_data_filled)
```

---

### 6. **Custom Aggregation**

You can pass custom aggregation functions like `sum`, `mean`, or even your own lambda functions:

#### Example: Weekly Aggregation with Multiple Metrics

```python
# Aggregate with multiple functions
weekly_stats = data.resample('W').agg(['mean', 'sum'])
print(weekly_stats)
```

Output:

```
            Sales      
             mean   sum
Date                    
2023-01-01  239.0   239
2023-01-08  283.0  1988
2023-01-15  399.0   798
```

---

### 7. **Plotting Resampled Data**

Resampling is commonly used to prepare time-series data for visualization:

```python
import matplotlib.pyplot as plt

# Plot original and resampled data
data['Sales'].plot(label='Daily Sales')
weekly_sales['Sales'].plot(label='Weekly Sales', linestyle='--')
plt.legend()
plt.show()
```

---

### 8. **`.dt` for Datetime Operations**

After resampling, you can use `.dt` to access specific attributes of a datetime object, such as month or year:

```python
data['Month'] = data.index.month
data['Year'] = data.index.year
```

