---
share: true
---
## Numpy Array
#### 1. Creating NumPy Arrays from Objects:
```python
my_list = [1,2,3]
my_list
np.array(my_list)
```

```python
my_matrix = [[1,2,3],[4,5,6],[7,8,9]]
my_matrix
np.array(my_matrix)
```

#### 2. Built-in Methods to create arrays:
* arange: Return evenly spaced values within a given interval
	`np.arange(start, stop, step) # stop is exclusive`
	`np.arange(0,11,2)`
* zeros and ones: Generate arrays of zeros or ones
	`np.zeros(3)`
	`np.zeros((5,3))`
	`np.ones(3)`
	`np.ones(3,2)`
* linspace: Return evenly spaced numbers over a specified interval
	Note that `.linspace()` *includes* the stop value. To obtain an array of common fractions, increase the number of items:
	`np.linspace(start, stop, num) # stop is inclusive`
	`np.linspace(0,10,11)`
* eye: Creates an identity matrix
	`np.eye(N) # Creates NxN identity matrix`
	`np.eye(4)`
#### 3. Random: Numpy also has lots of ways to create random number arrays:
* rand: Creates an array of the given shape and populates it with random samples from a uniform distribution over ``[0, 1)``
* A uniform distribution means every value in a range has an equal probability of being selected - like rolling a fair die where each number (1-6) has the same chance.
```python
np.random.rand(d0, d1, ..., dn) # Random samples from uniform distribution [0,1) 
# Examples 
np.random.rand(3) # 1D array with 3 random numbers 
np.random.rand(2,3) # 2x3 matrix of random numbers
```
* randn: Returns a sample (or samples) from the "standard normal" distribution [σ = 1]. Unlike **rand** which is uniform, values closer to zero are more likely to appear.
```python
np.random.randn(d0, d1, ..., dn) # Random samples from standard normal distribution (mean=0, std=1) 
# Examples 
np.random.randn(3) # 1D: 3 numbers from normal distribution 
np.random.randn(2,3) # 2D: 2x3 matrix from normal distribution
```
* randint: Returns random integers from `low` (inclusive) to `high` (exclusive).
```python
np.random.randint(low, high, size=None)  # Random integers from [low, high)

# Examples
np.random.randint(10)          # One random int [0,10)
np.random.randint(1,7)         # Like rolling a die [1,6]
np.random.randint(0,10,size=5) # Array of 5 random ints [0,10)
np.random.randint(1,7,(2,3))   # 2x3 array of dice rolls
```
* seed: Can be used to set the random state, so that the same "random" results can be reproduced.
```python
np.random.seed(42)
np.random.rand(4)
```
#### 4. Array Attributes and Methods
* Reshape: Returns an array containing the same data with a new shape
```python
arr = np.arange(25)
ranarr = np.random.randint(0,50,10)
arr.reshape(5,5) # 5*5=25 needs to be equal
ranarr.max() # Returns maximum value
ranarr.argmax() # Returns index of maximum value
ranarr.min()
ranarr.argmin()
```
* Shape: Shape is an attribute that arrays have (not a method)
```python
arr = np.array([[1,2,3],[4,5,6]])
arr.shape  # Returns tuple of dimensions: (2,3)

# Examples
np.zeros(5).shape         # (5,)     1D array
np.ones((3,4)).shape     # (3,4)    2D array
np.zeros((2,3,4)).shape  # (2,3,4)  3D array
```
* dtype: You can also grab the data type of the object in the array
```python
arr = np.array([1,2,3])
arr.dtype  # int64

# Common dtypes
np.array([1, 2]).dtype      # int64
np.array([1., 2.]).dtype    # float64
np.array(['a', 'b']).dtype  # <U1 (Unicode)
np.array([True]).dtype      # bool

# Specify dtype
np.array([1,2], dtype='float32')
```
