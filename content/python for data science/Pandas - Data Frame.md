---
share: true
---
#### Creating a DataFrame from Python Objects
A Pandas DataFrame consists of multiple Pandas Series that share index values.
```python
np.random.seed(101)
mydata = np.random.randint(0,101,(4,3))
myindex = ['CA','NY','AZ','TX']
mycolumns = ['Jan','Feb','Mar']
df = pd.DataFrame(data=mydata,index=myindex,columns=mycolumns)

df.info()
```

#### Obtaining Basic Information About DataFrame
```python
df.columns
df.index
df.head(3)
df.tail(3)
df.describe() #Statistical summary
df.describe().transpose()
```

#### Column Operations
Selection:
```python
df['total_bill']          # Single column → Series
df[['total_bill','tip']]  # Multiple columns → DataFrame
```
Modification:
```python
# Create new column
df['tip_pct'] = 100 * df['tip'] / df['total_bill']

# Round values
df['price_per_person'] = np.round(df['total_bill']/df['size'], 2)

# Delete column
df = df.drop('tip_pct', axis=1) 
```

Index Management:
```python
df.set_index('Payment ID', inplace=True)  # Set custom index
df.reset_index(inplace=True)              # Revert to default
```

#### Row Operations
Selection:
```python
df.iloc[0]        # By position → Series
df.loc['Sun2959'] # By index label → Series

df.iloc[0:4]              # Slice by position
df.loc[['Sun2959','Sun5260']]  # Specific labels
```
Modification:
```python
# Delete row
df.drop('Sun2959', axis=0)

# Add row (rarely used)
new_row = df.iloc[0]
df.append(new_row)
```

#### Pro Tips
1. **Path Check:** Use `pwd` and `ls` to verify file locations
    
2. **Axis Remember:**
    
    - `axis=0` → Rows (vertical)
        
    - `axis=1` → Columns (horizontal)
        
3. **Modification Best Practices:**
    
    - Use `inplace=True` or reassign (`df = df.drop(...)`)
        
    - Prefer vectorized operations over loops
* These changes are not permanent, unless like `df=df.drop('Sun2959', axis=0)`
* Sometimes, selecting logic is easier than dropping logic, so maybe we can use selecting logic more.
