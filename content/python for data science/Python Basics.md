---
share: true
title: Python Basics
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
In Python, since Python 3.7, regular dictionaries do maintain insertion order. This was actually made an official language feature in Python 3.7, though it was also true in Python 3.6 as an implementation detail.

A dictionary in programming is like your phone's contact list: 
- Each contact (key) has associated information (value)
- You look up information using the contact name
- Each contact name must be unique
- The information can be updated

Here's a simple Python example:

```python
# Creating a contacts dictionary
contacts = {
    "John": "+1-555-0123",
    "Alice": "+1-555-0456"
}

# Accessing a value
print(contacts["John"])  # +1-555-0123

# Adding new entry
contacts["Bob"] = "+1-555-0789"

# Updating existing entry
contacts["John"] = "+1-555-9999"

# Removing entry
del contacts["Alice"]
```

Key operations:
- Create: Use `{}` or `dict()`
- Access: Use square brackets `dict["key"]` or `.get("key")`
- Add/Update: `dict["key"] = value`
- Delete: `del dict["key"]`

Common use cases:
- Configuration settings
- Caching values
- Counting occurrences
- Mapping relationships

Let me demonstrate `keys()` and `items()` with a practical example:

```python
student_grades = {
    "Alice": 95,
    "Bob": 87,
    "Carol": 92
}

# keys() returns a view of all keys
print(student_grades.keys())  # dict_keys(['Alice', 'Bob', 'Carol'])

# Iterate through keys
for name in student_grades.keys():
    print(f"Student: {name}")

# items() returns key-value pairs as tuples
print(student_grades.items())  # dict_items([('Alice', 95), ('Bob', 87), ('Carol', 92)])

# Unpack pairs in loop
for name, grade in student_grades.items():
    print(f"{name}: {grade}")
```

Key points:
- `keys()`: Returns view object of dictionary keys
- `items()`: Returns view object of (key, value) pairs
- Both return views that update automatically when dictionary changes
- Commonly used in loops for accessing/processing dictionary data


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
#### Logic operators
`(1 > 2) and (2 < 3)`
`(1 > 2) or (2 < 3)`
`(1 == 2) or (2 == 3) or (4 == 4)`

#### If else
```
if 1 == 2:

	print('first')

elif 3 == 3:

	print('middle')

else:
	print('Last')
```

#### For loops
```
for jelly in seq:

	print(jelly+jelly)
```

#### While loops
```python
i = 1

while i < 5:

	print('i is: {}'.format(i))

	i = i+1
```

#### Range

Think of range like a ticket dispenser at a queue - it generates numbers in sequence. Here's the basic idea:

```python
for number in range(10):     # generates numbers 0-9
    print(number)
```

range has three common patterns:
- `range(10)` - counts from 0 to 9
- `range(1, 11)` - counts from 1 to 10
- `range(0, 10, 2)` - counts from 0 to 9, jumping by 2 each time (0,2,4,6,8)

It's mostly used in loops to generate a sequence of numbers, like a ticket system that helps you control "how many times" something should repeat.

`list(range(5))`

```python
x=[1,2,3,4]

out=[]

for item in x:

	out.append(item**2)

print(out)
```
`[item**2 for item in x]`
#### Function

A function is like a recipe:
```python
def make_sandwich(bread, filling):    # Ingredients (parameters)
    sandwich = bread + " with " + filling    # Instructions
    return sandwich    # Final dish

sandwich('whitebread','cucumbers')
```

Key points:
- Parameters are inputs (like ingredients)
- Function body contains instructions
- Return statement gives back the result
- You call it by name: `make_sandwich("rye", "cheese")`

Common patterns:
```python
# No parameters
def say_hello():
    print("Hello!")

# Multiple parameters
def total_price(price,taxrate):
	return price*(1+taxrate)

total_price(50,0.3)

# Default parameters
def greet(name="friend"):
    print(f"Hi {name}")
greet()
greet('yachen')
```

For function, it can have the default variable or not.

**The difference between print and return:**
`print()` is like speaking - it shows output to the user but doesn't pass information back to your program.

`return` is like handing something back - it gives a value back to the code that called the function, which can then use that value.

Example:
```python
def add(a, b):
    print(a + b)    # Just displays the result
    
def add_return(a, b):
    return a + b    # Gives back the result to use later

add(2, 3)           # Shows 5 but can't use the result
result = add_return(2, 3)  # Stores 5 in result for later use
```

Print is for displaying, return is for passing values between parts of your program.

#### String splitting

`st.split()` breaks a string into a list of substrings based on whitespace. For example:

```python
st = 'hello my name is Sam'
result = st.split()
print(result)  # ['hello', 'my', 'name', 'is', 'Sam']
# or just use
st.split()
```

You can also specify a different separator:
```python
email = "user@example.com"
username = email.split('@')[0]  # 'user'
```

```python
animals = "cat,dog,bird" 
print(animals.split(',')) # ['cat', 'dog', 'bird']
```

```python
tweet = 'Go Sports! #Sports'
tweet.split('#')
tweet.split('#')[1]
```


#### List del
Think of .pop() like taking the last card from a deck of cards - you're removing and getting that item in one action. This method is commonly used with lists (arrays in some languages) and works in two main ways:

1. Basic usage (no arguments):
```python
fruits = ['apple', 'banana', 'orange']
last_fruit = fruits.pop()  # removes and returns 'orange'
print(last_fruit)  # 'orange'
print(fruits)      # ['apple', 'banana']
```

2. With an index argument:
```python
fruits = ['apple', 'banana', 'orange']
second_fruit = fruits.pop(1)  # removes and returns 'banana'
print(second_fruit)  # 'banana'
print(fruits)        # ['apple', 'orange']
```

A key thing to understand is that .pop() actually does two things:
1. Removes the element from the list
2. Returns that element so you can use it

Common gotchas to watch out for:
- If you try to .pop() from an empty list, you'll get an IndexError
- When you .pop() an element, all subsequent elements shift left to fill the gap
- .pop() modifies the original list - if you just want to look at the last element without removing it, use list[-1] instead
#### Exercise
What is 7 to the power of 4?
`7**4`

Create a function that counts the number of times the word "dog" occurs in a string. Again ignore edge cases.
```python
def countDog(st):

	count = 0

	for word in st.lower().split():

		if word == 'dog':

			count += 1

	return count
```

