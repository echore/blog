---
share: true
---

## Basic Setup

```python
import numpy as np
import matplotlib.pyplot as plt

# If you're running this in a standard .py file (outside Jupyter),
# remember to use plt.show() at the end to display the plot window.
```

We typically import Matplotlib’s `pyplot` module under the alias `plt`. NumPy (`np`) is used for numerical operations (such as creating arrays of data for plotting).

Below, we define a simple dataset:

```python
x = np.arange(0,10)
y = 2 * x
```

---

## Legends

To label your plots, you can use `label="Some Label"` when calling `plot()` and then invoke `ax.legend()` to automatically create a legend. For example:

```python
fig = plt.figure()
ax = fig.add_axes([0,0,1,1])

ax.plot(x, x**2, label="x**2")
ax.plot(x, x**3, label="x**3")
ax.legend()  # Generate the legend
plt.show()
```

### Controlling Legend Location

- `ax.legend(loc=0)` lets Matplotlib choose the “best” location.
- Common integer codes for `loc`:
    - `loc=1`: upper right corner
    - `loc=2`: upper left corner
    - `loc=3`: lower left corner
    - `loc=4`: lower right corner

You can also specify a custom location, for example `loc=(1.1, 0.5)`.

---

## Setting Colors, Line Widths, and Line Types

Matplotlib provides many parameters for customizing your plots:

### 1. Quick "MATLAB-like" Syntax

```python
fig, ax = plt.subplots()
ax.plot(x, x**2, 'b.-')  # Blue line with dots
ax.plot(x, x**3, 'g--')  # Green dashed line
plt.show()
```

- `'b'` stands for blue, `'g'` for green, etc.
- `'.-'` indicates dotted lines, `'--'` indicates dashed lines, etc.

### 2. Using Keyword Arguments (Recommended)

This approach is more explicit and easier to read.

#### Colors by Name or Hex

```python
fig, ax = plt.subplots()

ax.plot(x, x+1, color="blue", alpha=0.5)   # Semi-transparent
ax.plot(x, x+2, color="#8B008B")          # Hex code for dark magenta
ax.plot(x, x+3, color="#FF8C00")          # Hex code for dark orange

plt.show()
```

- `color` accepts named colors or hex codes.
- `alpha` controls transparency (0.0 is fully transparent, 1.0 is fully opaque).

#### Line Widths

```python
fig, ax = plt.subplots(figsize=(12,6))

ax.plot(x, x-1, color="red", linewidth=0.25)
ax.plot(x, x-2, color="red", lw=0.50)
ax.plot(x, x-3, color="red", lw=1)
ax.plot(x, x-4, color="red", lw=10)

plt.show()
```

- Use `linewidth` or its shorthand `lw` to set line thickness.

#### Line Styles

```python
fig, ax = plt.subplots(figsize=(12,6))

ax.plot(x, x-1, color="green", lw=3, linestyle='-')   # Solid
ax.plot(x, x-2, color="green", lw=3, ls='-.')         # Dash-dot
ax.plot(x, x-3, color="green", lw=3, ls=':')          # Dotted
ax.plot(x, x-4, color="green", lw=3, ls='--')         # Dashed

plt.show()
```

Typical values for `linestyle` or `ls`:

- `'-'`: Solid
- `'-.'`: Dash-dot
- `':'`: Dotted
- `'--'`: Dashed

### Custom Dash Patterns

You can specify dash patterns to define the exact sequence of dashes and spaces:

```python
fig, ax = plt.subplots(figsize=(12,6))

lines = ax.plot(x, x+8, color="black", lw=5)
lines[0].set_dashes([10, 10])  # 10 points on, 10 points off

plt.show()
```

The format is `[on_1, off_1, on_2, off_2, ...]`.

---

## Markers

Matplotlib automatically connects data points with lines. To add markers at each data point:

```python
fig, ax = plt.subplots(figsize=(12,6))

ax.plot(x, x-1, marker='+', markersize=20)
ax.plot(x, x-2, marker='o', ms=20)            # using ms for marker size
ax.plot(x, x-3, marker='s', ms=20, lw=0)      # no line, just squares
ax.plot(x, x-4, marker='1', ms=20)

plt.show()
```

### Customizing Marker Appearance

```python
fig, ax = plt.subplots(figsize=(12,6))

ax.plot(x, x, color="black", lw=1, ls='-', 
        marker='s', markersize=20, 
        markerfacecolor="red", 
        markeredgewidth=8, 
        markeredgecolor="blue")

plt.show()
```

- `markerfacecolor`: The inner color of the marker.
- `markeredgecolor` and `markeredgewidth`: Outline color and thickness.
- `markersize` (`ms`): Marker size.
