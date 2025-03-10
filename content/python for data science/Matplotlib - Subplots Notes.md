---
share: true
---
### 1. Introduction

When you need to display multiple plots side by side (or in rows and columns), you can use Matplotlib’s **`subplots()`** function. It automatically creates both a **Figure** object (the container for your plots) and an array of **Axes** objects (the individual plots themselves). This makes it easier to manage multiple plots at once.

---

### 2. Basic Setup

```python
import matplotlib.pyplot as plt
import numpy as np

# Create some example data
a = np.linspace(0, 10, 11)  # 0 to 10, 11 points
b = a ** 4                 # a^4
x = np.arange(0, 10)
y = 2 * x
```

- `a`, `b`: Show a non-linear relationship (b = a^4).
- `x`, `y`: Show a simple linear relationship (y = 2x).

> **Note:**
> 
> - If you are running this in a non-Notebook environment (e.g., PyCharm, Sublime Text), remember to call `plt.show()` at the end to actually see your figures in a pop-up window.

---

### 3. Single Subplot with `plt.subplots()`

```python
fig, axes = plt.subplots()  
# By default, subplots() with no arguments gives you 1 row and 1 column.

axes.plot(x, y, 'r')
axes.set_xlabel('x')
axes.set_ylabel('y')
axes.set_title('Single Subplot Example')

# Display the plot
plt.show()
```

- `fig`: The Figure object, a container holding everything.
- `axes`: The Axes object, which you call `.plot()`, `.set_xlabel()`, etc. on.
- `'r'`: The line color (red) in the example above.

---

### 4. Multiple Subplots in Rows and Columns

#### 4.1 Creating a 1×2 Grid of Subplots

```python
fig, axes = plt.subplots(nrows=1, ncols=2)

# axes here is a 1D NumPy array of two Axes objects: [axes0, axes1]
axes[0].plot(a, b)        # left subplot
axes[0].set_title('Left Plot')

axes[1].plot(x, y)        # right subplot
axes[1].set_title('Right Plot')

plt.tight_layout()        # adjusts spacing to prevent overlap
plt.show()
```

- `axes[0]` and `axes[1]` are your two separate subplots.

#### 4.2 Creating a 2×2 Grid of Subplots

```python
fig, axes = plt.subplots(nrows=2, ncols=2)

# axes is now a 2D NumPy array: 
# [[axes00, axes01],
#  [axes10, axes11]]

axes[0][0].plot(a, b)
axes[0][0].set_title('Plot (0,0)')

axes[0][1].plot(b, a)
axes[0][1].set_title('Plot (0,1)')

axes[1][0].plot(x, y)
axes[1][0].set_title('Plot (1,0)')

axes[1][1].plot(y, x)
axes[1][1].set_title('Plot (1,1)')

plt.tight_layout()
plt.show()
```

> **Tip:** If the subplots overlap, use `plt.tight_layout()` or `fig.tight_layout()` to automatically adjust spacing.

---

### 5. Adjusting Figure Size and Titles

You can specify the figure size using the **`figsize=(width, height)`** argument in inches. You can also add a main title for the entire figure (sometimes called a “super title”).

```python
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12, 8))

# Plot on individual Axes:
axes[0][0].plot(a, b)
axes[0][0].set_title('0,0 Plot')

axes[0][1].plot(y, x)
axes[0][1].set_title('0,1 Plot')

axes[1][0].plot(b, a)
axes[1][0].set_title('1,0 Plot')

axes[1][1].plot(x, y)
axes[1][1].set_title('1,1 Plot')

# Set an overall figure title
fig.suptitle("Figure-Level Title", fontsize=16)

plt.tight_layout()  # Use this first
plt.show()
```

---

### 6. Manually Adjusting Spacing

Sometimes `tight_layout()` doesn’t give you exactly what you want. You can manually adjust spacing with `fig.subplots_adjust(...)`:

```python
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12, 8))

axes[0][0].plot(a, b)
axes[0][1].plot(y, x)
axes[1][0].plot(b, a)
axes[1][1].plot(x, y)

# Manually adjust the layout
fig.subplots_adjust(
    left=0.1,    # Default is 0.125
    right=0.9,   # Default is 0.9
    bottom=0.1,  # Default is 0.1
    top=0.9,     # Default is 0.9
    wspace=0.9,  # Width padding between subplots
    hspace=0.1   # Height padding between subplots
)

plt.show()
```

> - `left`, `right`, `bottom`, `top` “stretch” the margins of your entire figure.
> - `wspace`, `hspace` control the blank space between subplots.

---

### 7. Saving a Figure

To save your figure to a file, call **`fig.savefig()`**:

```python
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12, 8))

axes[0][0].plot(a, b)
axes[0][1].plot(y, x)
axes[1][0].plot(b, a)
axes[1][1].plot(x, y)

# Save before or after plt.show()
fig.savefig('subplots.png', bbox_inches='tight')

plt.show()
```

- `bbox_inches='tight'` crops any extra whitespace around your figure.

---

## Key Takeaways

1. **`fig, axes = plt.subplots()`** provides both the figure and axes automatically.
2. You can create multiple rows and columns by setting `nrows` and `ncols`.
3. Access individual Axes via indexing:
    - **1×2** subplots: `axes[0]`, `axes[1]`
    - **2×2** subplots: `axes[row][col]`
4. Use **`tight_layout()`** for automatic spacing or **`fig.subplots_adjust()`** for more control.
5. The **Figure** is the overall container; each **Axes** is an individual plotting area.

---

### Additional Reading

- [Official Matplotlib Subplots Documentation](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.subplots.html)
- [Adjusting Spacing with subplots_adjust()](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.subplots_adjust.html)

---

> **Analogy**: Think of the **Figure** as a large sheet of paper, and each **Axes** is a smaller “panel” or “box” on that paper. Each panel can contain one or more plots. The `subplots()` function helps you quickly cut that sheet into a grid of these panels.

