---
share: true
---

#### Print
```
print("My name is {}, My number is {}".format('Rose','10'))
print("First {x}, Second {y}".format(x="xxx",y="yyy"))
```

```
num = 12
name = 'Sam'
```

```
print('My number is: {one}, and my name is:{two}'.format(one=num,two=name))
```

#### List
```
my_list = ['a','b','c']
my_list.append('d')
my_list[1:]
my_list[0] = 'NEW'
```

```
nest = [1,2,3,[4,5,['target']]]
nest[3][2][0]
```

#### Dictionaries
```
d = {'key1':'item1','key2':'item2'}
d['key1']
```
In Python, since Python 3.7, regular dictionaries do maintain insertion order. This was actually made an official language feature in Python 3.7, though it was also true in CPython 3.6 as an implementation detail.

#### Booleans 
0- False 1- True

#### tuples
Tuples are immutable sequences in Python, meaning once created, their elements cannot be changed.
```
# Creating tuples
empty_tuple = ()
single_element = (1,)    # Note the comma - it's required for single-element tuples
multiple_elements = (1, 2, 3)
# You can also create tuples without parentheses
also_tuple = 1, 2, 3
```

```
# Immutable - cannot be modified after creation
coords = (3, 4)
coords[0] = 5    # TypeError: 'tuple' object does not support item assignment

# Indexing and slicing work like lists
numbers = (0, 1, 2, 3, 4)
print(numbers[0])     # 0
print(numbers[-1])    # 4
print(numbers[1:3])   # (1, 2)

# Can contain different data types
mixed = (1, "hello", True, 3.14)

# Useful for multiple assignments
x, y = (10, 20)  # Tuple unpacking
```

```
# Count occurrences
numbers = (1, 2, 2, 3, 2)
print(numbers.count(2))    # 3

# Find index of element
print(numbers.index(3))    # 3

# Length
print(len(numbers))        # 5

# Concatenation
tuple1 = (1, 2)
tuple2 = (3, 4)
combined = tuple1 + tuple2  # (1, 2, 3, 4)

# Repetition
repeated = tuple1 * 2      # (1, 2, 1, 2)
```

Why use tuples over lists?

1. Tuples are immutable, making them safer for data that shouldn't change
2. Tuples are more memory efficient than lists
3. Tuples can be used as dictionary keys
4. They signal intent in your code (showing data that won't change)

#### sets
```
# Sets are unordered {1, 2, 3} == {3, 1, 2} # True # Sets only store unique values numbers = {1, 2, 2, 3} 
print(numbers) # {1, 2, 3}
```