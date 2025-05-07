---
share: true
---

These are some of the problems I encountered and the solutions I found when doing the project.：

The size of your plot isn't changing because you're using `sns.displot()` (a Seaborn figure-level function) after setting the figure size with `plt.figure()`. 

### The Issue:
- `plt.figure(figsize=(11,4))` creates a new Matplotlib figure with the specified size.
- However, `sns.displot()` is a **figure-level** Seaborn function, which means it creates its own new figure when called, ignoring any existing figures (including the one you just created with `plt.figure()`).

### Solutions:
1. **Use `sns.histplot()` (axes-level function) instead of `sns.displot()`:**
   ```python
   plt.figure(figsize=(11, 4))
   sns.histplot(data=Rotten_Diff, kde=True)
   plt.xlabel("Rotten_Diff")
   plt.title("RT Critics Score minus RT User Score")
   plt.show()
   ```
   `sns.histplot()` is an axes-level function and will respect the figure size you set with `plt.figure()`

### Key Difference:
- **Figure-level functions** (`sns.displot`, `sns.catplot`, `sns.relplot`, etc.) create their own figure and ignore `plt.figure()`. You control their size with `height` and `aspect`.
- **Axes-level functions** (`sns.histplot`, `sns.scatterplot`, `sns.barplot`, etc.) draw on the currently active Matplotlib axes (or create one if none exists). You can control their size with `plt.figure(figsize=(width, height))`.


If you want to get the **top 5 values** from one column and see their **associated values** in another column, you can use Pandas operations like `nlargest()` or `sort_values()`. Here's how to do it:

### Example Scenario:

- Suppose you have a DataFrame `df` with two columns:
    
    - `column_A`: The column from which you want the top 5 values.
        
    - `column_B`: The column whose associated values you want to extract.
        

### Methods to Achieve This:

#### 1. Using `nlargest()` (Recommended for Top N Values)

```
top_5 = df.nlargest(5, 'column_A')[['column_A', 'column_B']]
```

- This directly gives the rows with the **5 largest values in `column_A`**, along with their corresponding `column_B` values.