---
share: true
---

## Python `datetime` Review

The `datetime` library in Python helps manage and manipulate date and time. Here's a quick review:

### Creating a `datetime` object

```python
from datetime import datetime

# Specify year, month, day, and optionally hour, minute, and second
my_year = 2017
my_month = 1
my_day = 2
my_hour = 13
my_minute = 30
my_second = 15

# Creating a basic date (defaults to 00:00 time)
my_date = datetime(my_year, my_month, my_day)
print(my_date)

# Creating a full datetime with time
my_date_time = datetime(my_year, my_month, my_day, my_hour, my_minute, my_second)
print(my_date_time)
```

### Accessing parts of a `datetime` object

You can retrieve specific components like the day or hour:

```python
print(my_date.day)       # 2
print(my_date_time.hour) # 13
```

---

## Pandas and Datetime

Pandas makes it easy to work with datetime objects, especially when dealing with time-series data.

### Converting Strings to Datetime

Often, dates in datasets are stored as strings. Use `pd.to_datetime` to convert them to datetime objects.

```python
import pandas as pd

# Example Series with dates
myser = pd.Series(['Nov 3, 2000', '2000-01-01', None])
print(myser)

# Convert to datetime
converted = pd.to_datetime(myser)
print(converted)

# Handling ambiguous dates (e.g., European format)
euro_date = '10-12-2000'
print(pd.to_datetime(euro_date, dayfirst=True))  # Interprets as 10th December 2000
```

#### Custom Time String Formatting

If the date format is non-standard, you can specify it explicitly using the `format` parameter. This can improve parsing performance.

```python
style_date = '12--Dec--2000'
parsed_date = pd.to_datetime(style_date, format='%d--%b--%Y')
print(parsed_date)
```

Reference for format codes: [Python Datetime Format Codes](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes)

---

## Working with Time-Series Data

### Example Dataset: Retail Sales

Let's load a dataset:

```python
sales = pd.read_csv('RetailSales_BeerWineLiquor.csv')
print(sales.head())

# Convert DATE column to datetime
sales['DATE'] = pd.to_datetime(sales['DATE'])
print(sales.dtypes)
```

### Setting Datetime Index

For time-series operations, set the datetime column as the index:

```python
sales = sales.set_index("DATE")
print(sales.head())
```

### Attempt to Parse Dates Automatically

The `parse_dates` parameter is a powerful feature in Pandas' data reading functions (like `pd.read_csv` or `pd.read_excel`) that allows you to automatically **convert columns containing date strings into datetime objects** when loading the data. This saves you the extra step of manually calling `pd.to_datetime()` on those columns after loading the file.

```python
sales = pd.read_csv('RetailSales_BeerWineLiquor.csv',parse_dates=[0])
```
---

## [[Resampling Time-Series Data|Resampling Time-Series Data]]

The `resample()` method is used for aggregating data based on time frequency.

### Resampling Rules (Offset Aliases)

Common aliases for resampling:

- `A`: Year-end frequency
- `Q`: Quarter-end frequency
- `M`: Month-end frequency
- `W`: Weekly frequency
- `D`: Daily frequency

Full list: [Pandas Offset Aliases](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#offset-aliases)

### Example: Yearly Means

```python
# Resample by year and calculate the mean
yearly_mean = sales.resample('A').mean()
print(yearly_mean)
```

### Using the `.dt` Accessor

Once a column is in datetime format, you can access various attributes and methods:

```python
sales = sales.reset_index()

# Extracting components
print(sales['DATE'].dt.month)        # Extract month
print(sales['DATE'].dt.is_leap_year) # Check for leap year
```
