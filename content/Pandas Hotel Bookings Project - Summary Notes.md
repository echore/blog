---
share: true
---

## 🚧 Data Preparation

**Load Data:**

```python
import pandas as pd
hotels = pd.read_csv("hotel_booking_data.csv")
hotels.head()
```

**Check Data Info:**

```python
hotels.info()
```

---

## ✅ Task Solutions and Explanations

### 1. **Number of rows in the dataset**

```python
len(hotels)
```

### 2. **Checking missing data and identifying columns with most missing data**

```python
hotels.isnull().sum()
# "company" column has the most missing values
```

**Detailed Check:**

```python
missing_company = hotels['company'].isna().sum()
print(f"Yes, missing data, company column missing: {missing_company} rows.")
```

### 3. **Drop the "company" column**

```python
hotels.drop('company', axis=1, inplace=True)
# my answer
hotels.dropna(subset=['company'])
```

---

## 🔥 Data Analysis and Insights

### 4. **Top 5 most common country codes**

```python
hotels['country'].value_counts().head(5)
```

### 5. **Highest ADR (Average Daily Rate)**

- Person who paid highest ADR and the amount:

```python
hotels.sort_values('adr', ascending=False)[['adr', 'name']].iloc[0]
# my answer
hotels.nlargest(1, 'adr')[['name','adr']]
# or
hotels.iloc[hotel['adr].idmax()]
```

### 6. **Mean ADR across all bookings**

```python
round(hotels['adr'].mean(), 2)
# mine
hotels['adr'].mean().round(2)
```

---

## 🗓️ Stay Duration Analysis

### 7. **Average length of stay (in nights)**

- Calculate the total nights by summing weekdays and weekends:

```python
hotels['total_stay_days'] = hotels['stays_in_week_nights'] + hotels['stays_in_weekend_nights']
round(hotels['total_stay_days'].mean(), 2)
# mine
(hotels['stays_in_weekend_nights'].mean() + hotels['stays_in_week_nights'].mean()).round(2)
```

### 8. **Average total cost per stay**

- Compute total cost (`total_paid`) by multiplying ADR by total nights:

```python
hotels['total_paid'] = hotels['adr'] * hotels['total_stay_days']
round(hotels['total_paid'].mean(), 2)
```

---

## 🌟 Special Requests & Guest Analysis

### 9. **Guests who made exactly 5 special requests**

```python
hotels[hotels['total_of_special_requests'] == 5][['name', 'email']]
```

### 10. **Percentage of repeat guests**

```python
repeat_percentage = round(100 * (hotels['is_repeated_guest'] == 1).sum() / len(hotels), 2)
repeat_percentage
# mine
((len(hotels[hotels['is_repeated_guest'] == True]) / len(hotels)) * 100)
```

---

## 📝 Further Guest Information Analysis

### 11. **Top 5 most common last names**

- Extract the last names using lambda function:

```python
hotels['name'].apply(lambda name: name.split()[1]).value_counts().head(5)
#mine
hotels['name'].str.split(' ').str[1].value_counts().head(5)
```

### 12. **Guests with the highest number of children and babies**

```python
hotels['total_kids'] = hotels['babies'] + hotels['children']
hotels.sort_values('total_kids', ascending=False)[['name', 'adults', 'total_kids', 'babies', 'children']].head(3)
# mine
hotels['total_kids'] = hotels['babies'] + hotels['children']
top_hotels = hotels.nlargest(3, 'total_kids')
result = top_hotels[['name', 'adults', 'total_kids', 'babies', 'children']]
result
```

### 13. **Top 3 most common phone number area codes**

- Extract area code (first 3 digits) from phone numbers:

```python
hotels['phone-number'].str[:3].value_counts().head(3)
```

---

## 📅 Arrival Date Analysis

### 14. **Number of arrivals between 1st and 15th of each month**

- Efficient one-line solution:

```python
hotels['arrival_date_day_of_month'].apply(lambda day:day in range(1, 16)).sum()
# mine
(hotels['arrival_date_day_of_month'][(hotels['arrival_date_day_of_month'] >= 1) & (hotels['arrival_date_day_of_month'] <= 15)]).sum()
```

---

## 🚀 Advanced Task (Bonus)

### 15. **Count of arrivals per weekday**

- Combine date columns and convert to datetime for weekday extraction:

```python
import numpy as np

def convert(day,month,year):
	return f'{day}-{month}-{year}'
hotels['date'] = np.vectorize(convert)(hotels['arrival_date_day_of_month'],hotels['arrival_date_month'],hotels['arrival_date_year'])
hotels['date'] = pd.to_datetime(hotels['date'])
hotels['date'].dt.day_name().value_counts()
```

---

## 🧠 Key Points & Reminders:

- Use `hotels.info()` and `hotels.describe()` for initial data inspection.
- `value_counts()` is powerful for quick categorical insights.
- `apply()` with lambda is excellent for string or numeric transformations.
- Combining date parts into a single datetime column allows more advanced time-based analysis.
