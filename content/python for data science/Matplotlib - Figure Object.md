---
share: true
---

## 3. Creating a Figure

The Object-Oriented approach requires creating a **Figure** object and adding **Axes** to it.

### 3.1 Basic Figure with Axes

```python
fig = plt.figure()  # Creates an empty figure

# Adding a set of axes: [left, bottom, width, height] (range: 0 to 1)
axes = fig.add_axes([0, 0, 1, 1])  

# Plotting on the axes
axes.plot(x, y)

plt.show()
```

🔹 `fig.add_axes([0, 0, 1, 1])`:

- `left, bottom`: Position of the axes (0 to 1)
- `width, height`: Size of the axes (0 to 1)
- left and bottom: refer to the position of the lower left corner of the axis in the entire Figure canvas (relative ratio, 0 means the far left/bottom, 1 means the far right/top).
- width and height: refer to the width and height of the axis, relative to the ratio of the entire Figure canvas, the maximum can be 1, but it can exceed 1, but it will overflow the Figure canvas range

### 3.2 Different Data on Another Axes

```python
fig = plt.figure()
axes = fig.add_axes([0, 0, 1, 1])
axes.plot(a, b)  # Plotting `a, b`
plt.show()
```

---

## 4. Adding Multiple Axes 🎭

We can add multiple axes within the same figure.

### 4.1 Small Plot Inside a Bigger Plot

```python
fig = plt.figure()

axes1 = fig.add_axes([0, 0, 1, 1])    # Main figure (large)
axes2 = fig.add_axes([0.2, 0.2, 0.5, 0.5])  # Smaller inset figure

# Plot on larger figure
axes1.plot(a, b)
axes1.set_xlabel('X Label')
axes1.set_ylabel('Y Label')
axes1.set_title('Big Figure')

# Plot on smaller figure
axes2.plot(a, b)
axes2.set_title('Small Figure')

plt.show()
```

🎯 **Key Idea:**  
This method gives complete control over positioning.

---

## 5. Adjusting Inset Axes 🖼️

### 5.1 Moving and Zooming the Smaller Figure

```python
fig = plt.figure()

axes1 = fig.add_axes([0, 0, 1, 1])      # Large figure
axes2 = fig.add_axes([0.2, 0.5, 0.25, 0.25])  # Small figure moved to top-left

# Large Figure
axes1.plot(a, b)
axes1.set_xlabel('X Label')
axes1.set_ylabel('Y Label')
axes1.set_title('Big Figure')

# Small Figure (Zoomed In)
axes2.plot(a, b)
axes2.set_xlim(8,10)
axes2.set_ylim(4000,10000)
axes2.set_xlabel('X')
axes2.set_ylabel('Y')
axes2.set_title('Zoomed In')

plt.show()
```

🛠 **Adjustments in `axes2`**

- `set_xlim(8,10)`: Focus on **x-range [8,10]**
- `set_ylim(4000,10000)`: Focus on **y-range [4000,10000]**

---

## 6. Multiple Inset Plots 📊

We can keep adding more axes!

```python
fig = plt.figure()

axes1 = fig.add_axes([0, 0, 1, 1])       # Full figure
axes2 = fig.add_axes([0.2, 0.5, 0.25, 0.25])  # Inset 1
axes3 = fig.add_axes([1, 1, 0.25, 0.25])  # Inset 2 (top-right corner)

# Large Figure
axes1.plot(a, b)
axes1.set_xlabel('X Label')
axes1.set_ylabel('Y Label')
axes1.set_title('Big Figure')

# Inset 1
axes2.plot(a, b)
axes2.set_xlim(8,10)
axes2.set_ylim(4000,10000)
axes2.set_xlabel('X')
axes2.set_ylabel('Y')
axes2.set_title('Zoomed In')

# Inset 2 (new one)
axes3.plot(a, b)
axes3.set_title('Another Small Figure')

plt.show()
```

---

## 7. Adjusting Figure Size & Resolution 📏

We can specify **size and resolution** while creating the figure.

```python
fig = plt.figure(figsize=(12,8), dpi=100)  # Width=12 inches, Height=8 inches, DPI=100
axes1 = fig.add_axes([0, 0, 1, 1])
axes1.plot(a, b)
plt.show()
```

📌 **Commonly used options**

- `figsize=(width, height)`: Controls figure size.
- `dpi=resolution`: Higher values make the image clearer.

---

## 8. Exporting Figures 📂

We can save figures as image files.

### 8.1 Saving as a PNG

```python
fig = plt.figure()
axes1 = fig.add_axes([0, 0, 1, 1])
axes1.plot(a, b)
axes1.set_xlabel('X')

fig.savefig('figure.png', bbox_inches='tight')  # Saves as 'figure.png'
```

🔹 `bbox_inches='tight'` ensures the image is cropped properly.

### 8.2 Another Example

```python
fig = plt.figure(figsize=(12,8))
axes1 = fig.add_axes([0, 0, 1, 1])  
axes2 = fig.add_axes([1, 1, 0.25, 0.25])  

axes1.plot(x, y)
axes2.plot(x, y)

fig.savefig('test.png', bbox_inches='tight')
```

---

## Summary ✨

|Feature|Method|
|---|---|
|**Create Figure**|`fig = plt.figure()`|
|**Add Axes**|`fig.add_axes([left, bottom, width, height])`|
|**Set Labels**|`axes.set_xlabel('X')`, `axes.set_ylabel('Y')`|
|**Set Title**|`axes.set_title('Title')`|
|**Plot Data**|`axes.plot(x, y)`|
|**Zoom in on Axes**|`axes.set_xlim(start, end)`, `axes.set_ylim(start, end)`|
|**Adjust Figure Size**|`fig = plt.figure(figsize=(width, height), dpi=resolution)`|
|**Save Figure**|`fig.savefig('filename.png', bbox_inches='tight')`|

📌 **When to use Object-Oriented Matplotlib?**

- When dealing with **multiple plots** in one figure.
- When **precise positioning** of axes is needed.
- When **embedding plots** inside other figures.
