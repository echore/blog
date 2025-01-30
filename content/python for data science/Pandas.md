---
share: true
---

## Series
#### Index and Data Lists:
We can create a Series from Python lists (also from NumPy arrays)
```python
myindex = ['USA','Canada','Mexico']
mydata = [1776,1867,1821]
myser = pd.Series(data=mydata) # it can give default numeric index
myser1 = pd.Series(data=mydata,index=myindex) # Access values by label instead of just position
myser1[0] 
myser1['USA'] 
```

#### From NumPy Arrays
```python
ran_data = np.random.randint(0,100,4)
names = ['Andrew','Bobo','Claire','David']
ages = pd.Series(ran_data, names)
```

#### From Dictionaries
```python
ages = {'Sammy':5, 'Frank':10, 'Spike':7}
age_series = pd.Series(ages)
```

---

### Key Features

#### Named Index
```python
sales_Q1 = pd.Series({'Japan': 80, 'China': 450, 'India': 200, 'USA': 250})
```

#### Accessing Values
```python
# By label
sales_Q1['Japan']  # Returns 80

# By position
sales_Q1[0]  # Returns 80
```

####  Important Attributes
```python
sales_Q1.keys()  # Returns index labels
sales_Q1.values  # Returns array of values
```

---

### Operations

####  Scalar Operations
```python
sales_Q1 * 2  # Multiplies all values by 2
sales_Q2 / 100  # Divides all values by 100
```

####  Series-to-Series Operations
```python
# Automatic alignment by index
sales_Q1 + sales_Q2  # NaN for mismatched indices

# Handling missing values
sales_Q1.add(sales_Q2, fill_value=0)
```

 Once we did the Operations, the datatype will transform into float.


> 🚨 **Caution**  
> - Case-sensitive: `sales_Q1['usa']` ≠ `sales_Q1['USA']`  
> - Exact matches required: `sales_Q1['USA ']` (with space) will error  
> - Non-existent keys throw KeyError


