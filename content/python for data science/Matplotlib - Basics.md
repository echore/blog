---
share: true
---

## Basic Plot Example

Using **NumPy** to create simple data and plot a line graph:

```python
import numpy as np
import matplotlib.pyplot as plt

# Generate data
x = np.arange(0, 10)  # Array: 0 to 9
y = 2 * x  # y = 2 * x

# Plotting
plt.plot(x, y)  # Line plot
plt.xlabel('X Axis Label')  # X-axis label
plt.ylabel('Y Axis Label')  # Y-axis label
plt.title('Basic Line Plot')  # Title
plt.xlim(0, 6)  # Set X-axis range
plt.ylim(0, 12)
plt.show()  # Display the figure
```

### 🔍 Breakdown:

- `plt.plot(x, y)`: Creates a line plot
- `plt.xlabel('X Axis Label')`: Adds a label to the X-axis
- `plt.ylabel('Y Axis Label')`: Adds a label to the Y-axis
- `plt.title('Basic Line Plot')`: Adds a title to the plot
- `plt.show()`: Displays the figure (essential for non-Jupyter environments)
- `plt.xlim(0,6)`: Restricts the X-axis range to **0 to 6**
- `plt.ylim(0,12)`: Restricts the Y-axis range to **0 to 12**

---
## Exporting a Plot

Matplotlib allows you to **save plots** in various formats:

```python
plt.plot(x, y)
plt.savefig('example.png')  # Save as PNG
```

📌 **Additional options**:

- `plt.savefig('example.png', dpi=300)`: Higher **resolution (300 dpi)**
- `plt.savefig('example.pdf')`: Save as **PDF**
- `plt.savefig('example.svg')`: Save as **SVG (vector format)**

---

### 🎯 Summary:

- **Matplotlib** is a powerful, customizable library for data visualization
- **Basic workflow**: Import → Generate data → `plt.plot()` → Add labels/titles → `plt.show()`
- **Customization**: Adjust axis limits (`xlim()`, `ylim()`), labels (`xlabel()`, `ylabel()`), and title (`title()`)
- **Exporting**: Use `plt.savefig()` to save in multiple formats

