---
share: true
---

#### **Task 1: Creating Data from an Equation**

We will plot **Einstein’s mass-energy equivalence equation**:

**Step 1: Generate Data Using NumPy**
We create an array m of **mass values (0g - 10g, evenly spaced)** and compute energy E using the equation.

```
import numpy as np

# Define mass values from 0 to 10 grams (11 evenly spaced points)
m = np.linspace(0, 10, 11)
print(f"The array m:\n{m}")

# Speed of light (approximate value in m/s)
c = 3 * 10**8  

# Calculate Energy using E = mc^2
E = m * c**2
print(f"The array E:\n{E}")
```

**Step 2: Plot E = mc²**
Now, we **plot the equation** using Matplotlib.

```
import matplotlib.pyplot as plt

# Plot Energy vs Mass
plt.plot(m, E, color='red', lw=5)

# Labels and Title
plt.title("E=mc²")
plt.xlabel("Mass in Grams")
plt.ylabel("Energy in Joules")

# Set x-axis limits
plt.xlim(0, 10)

# Show plot
plt.show()
```

**Bonus: Logarithmic Scale**

We **plot on a logarithmic scale** for better visualization and add a grid.

```
# Create plot
plt.plot(m, E, color='red', lw=5)

# Labels and Title
plt.title("E=mc²")
plt.xlabel("Mass in Grams")
plt.ylabel("Energy in Joules")

# Set x-axis limits
plt.xlim(0, 10)

# Set y-axis to log scale
plt.yscale("log")

# Add a grid along y-axis ticks
plt.grid(which='both', axis='y')

# Show plot
plt.show()
```

#### **Task 2: Yield Curve Data**

A **yield curve** shows how interest rates vary with time to maturity. Below is **U.S. Treasury yield curve data** for **July 16, 2007** and **July 16, 2020**.

**Step 1: Define Yield Curve Data**

```
# Labels for bond maturity periods
labels = ['1 Mo', '3 Mo', '6 Mo', '1 Yr', '2 Yr', '3 Yr', '5 Yr', '7 Yr', '10 Yr', '20 Yr', '30 Yr']

# Interest rates for July 16, 2007
july16_2007 = [4.75, 4.98, 5.08, 5.01, 4.89, 4.89, 4.95, 4.99, 5.05, 5.21, 5.14]

# Interest rates for July 16, 2020
july16_2020 = [0.12, 0.11, 0.13, 0.14, 0.16, 0.17, 0.28, 0.46, 0.62, 1.09, 1.31]
```

**Step 2: Plot Both Curves on the Same Figure**

```
# Create Figure
fig = plt.figure()

# Add axes
axes = fig.add_axes([0, 0, 1, 1])  # left, bottom, width, height (range 0 to 1)

# Plot both yield curves
axes.plot(labels, july16_2007, label='July 16, 2007')
axes.plot(labels, july16_2020, label='July 16, 2020')

# Add Legend
plt.legend()

# Show plot
plt.show()
```

**Step 3: Move the Legend Outside the Plot**

By default, the legend is inside the plot, but we can **move it outside**.

```
# Create Figure
fig = plt.figure()

# Add axes
axes = fig.add_axes([0, 0, 1, 1])

# Plot yield curves
axes.plot(labels, july16_2007, label='July 16, 2007')
axes.plot(labels, july16_2020, label='July 16, 2020')

# Move legend outside
plt.legend(loc=(1.04, 0.5))

# Show plot
plt.show()
```

**Step 4: Use Subplots to Separate the Years**

Instead of plotting both years on the same graph, we can **use subplots** for clarity.

```
# Create subplots (2 rows, 1 column)
fig, axes = plt.subplots(nrows=2, ncols=1, figsize=(12, 8))

# Plot 2007 data
axes[0].plot(labels, july16_2007, label='July 16, 2007')
axes[0].set_title("July 16, 2007")

# Plot 2020 data
axes[1].plot(labels, july16_2020, label='July 16, 2020')
axes[1].set_title("July 16, 2020")

# Show plots
plt.show()
```


**Bonus Challenge: Twin Axes for Yield Curves**
We can **overlay both yield curves** using **twin axes** to maintain separate scales.

```
# Create figure
fig, ax1 = plt.subplots(figsize=(12, 8))

# Left axis (2007, Blue)
ax1.plot(labels, july16_2007, lw=2, color="blue")
ax1.set_ylabel("2007", fontsize=18, color="blue")
ax1.spines['left'].set_color('blue')
ax1.spines['left'].set_linewidth(4)
ax1.tick_params(axis='y', colors='blue', labelsize=15)

# Create right axis
ax2 = ax1.twinx()

# Right axis (2020, Red)
ax2.plot(labels, july16_2020, lw=2, color="red")
ax2.set_ylabel("2020", fontsize=18, color="red")
ax2.spines['right'].set_color('red')
ax2.spines['right'].set_linewidth(4)
ax2.tick_params(axis='y', colors='red', labelsize=15)

# Title
ax1.set_title("July 16th Yield Curves", fontsize=20)

# Show plot
plt.show()
```



  
