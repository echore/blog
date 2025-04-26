---
share: true
---

### 🖼️ **Plot 1 – Multiple Lines (One per Species)**
![[Pasted image 20250424165936.png|Pasted image 20250424165936.png]]

```r
ggplot(
  data = penguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g, color = species)
) +
  geom_point() +
  geom_smooth(method = "lm")
```

**What happens here:**

- `color = species` is defined **globally**.
    
- This means both:
    
    - The **points** are colored by species ✅
        
    - The **lines** are also colored by species ❗
        
- So, **`geom_smooth()` draws one line per species**.
    

📊 You get: **3 regression lines** (1 for each species), each in a different color.

---

### 🖼️ **Plot 2 – Single Line (All Species Together)**
![[Pasted image 20250424165920.png|Pasted image 20250424165920.png]]

```r
ggplot(
  data = penguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g)
) +
  geom_point(mapping = aes(color = species)) +
  geom_smooth(method = "lm")
```

**What changes:**

- `color = species` is now inside **`geom_point()` only**.
    
- So:
    
    - The **points** are still colored by species ✅
        
    - The **line** is drawn **once for all data** ❗ (no grouping by species)
        

📊 You get: **1 regression line**, using all data regardless of species.

---

### 🧠 Quick Rule to Remember:

|Where is `color = species`?|What you get|
|---|---|
|Global (in `ggplot()`)|Colors everything (points & lines) = ➕ grouped smooth lines|
|Local (in `geom_point()`)|Only colors the points = ➕ one unified line|


![[Pasted image 20250424171042.png|Pasted image 20250424171042.png]]
```
ggplot(
  data = penguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g)
) +
  geom_point(aes(color = species, shape = species)) +
  geom_smooth(method = "lm") +
  labs(
    title = 'Body mass and flipper length',
    subtitle = 'Dimensions for Adelie, Chinstrap, and Gentoo Penguins',
    x = "Flipper length (mm)", y = "Body mass (g)",
    color = 'species',shape='species'
  ) +
  scale_color_colorblind()
```


I asked AI to organize the notes based on my solution:

---

## 1.2.5 Exercises (palmerpenguins)

### 1. How many rows and columns are in `penguins`?

```r
nrow(penguins)  # number of observations (rows)
ncol(penguins)  # number of variables  (columns)
```

- **Answer**:
    
    - Rows: `nrow(penguins)`
        
    - Columns: `ncol(penguins)`
        

---

### 2. What does `bill_depth_mm` describe?

```r
?penguins
```

- **Description**:  
    `bill_depth_mm` = depth of the penguin’s bill (beak) in millimeters, measured at the thickest point.
    

---

### 3. Scatterplot: `bill_depth_mm` vs. `bill_length_mm`
![[Pasted image 20250425210439.png|Pasted image 20250425210439.png]]

```r
library(ggplot2)

ggplot(penguins, aes(x = bill_length_mm, y = bill_depth_mm)) +
  geom_point(aes(color = species, shape = species), alpha = 0.7) +
  geom_smooth(method = "lm", se = FALSE) +
  labs(
    title = "Bill Depth vs. Bill Length by Species",
    x     = "Bill Length (mm)",
    y     = "Bill Depth (mm)",
    color = "Species",
    shape = "Species"
  )
```

- **Relationship**:  
    There’s a moderate positive correlation—penguins with longer bills also tend to have deeper bills. Patterns differ by species.
    

---

### 4. Scatterplot of `species` vs. `bill_depth_mm`
![[Pasted image 20250425210456.png|Pasted image 20250425210456.png]]

```r
ggplot(penguins, aes(x = species, y = bill_depth_mm)) +
  geom_boxplot(aes(color = species)) +
  labs(
    title = "Distribution of Bill Depth by Species",
    x     = "Species",
    y     = "Bill Depth (mm)"
  )
```

- **What happens**:  
    A plain scatter (`geom_point`) stacks points and overlaps heavily.
    
- **Better choice**:  
    `geom_boxplot()` (or `geom_violin()`) to summarize each species’ distribution.
but actually answer belike:
![[Pasted image 20250425210658.png|Pasted image 20250425210658.png]]
```
ggplot(
  data = penguins, 
  aes(x = bill_depth_mm, y = species)
) + 
  geom_point()
```

### 5. Why does this give an error?

```r
ggplot(data = penguins) +
  geom_point()
```

- **Error**:  
    `geom_point()` needs at least `aes(x, y)`; none were provided.
    
- **Fix**:  
    Supply aesthetics, for example:
    
    ```r
    ggplot(penguins, aes(x = bill_length_mm, y = bill_depth_mm)) +
      geom_point()
    ```
    

---

### 6. The `na.rm` argument in `geom_point()`

- **What it does**:  
    `na.rm = TRUE` removes any rows with `NA` in the mapped aesthetics before plotting.
    
- **Default**:  
    `na.rm = FALSE` (will warn or drop NAs with a message).
    

```r
ggplot(penguins, aes(x = bill_length_mm, y = bill_depth_mm)) +
  geom_point(na.rm = TRUE) +
  labs(
    title    = "Bill Measurements (NAs removed)",
    subtitle = "Using na.rm = TRUE",
    x        = "Bill Length (mm)",
    y        = "Bill Depth (mm)"
  )
```

---

### 7. Add a caption

Use `labs(caption = "…")`, for example:

```r
+ labs(caption = "Data come from the palmerpenguins package.")
```

---

### 8. Recreate this visualization

> **Task**: scatterplot of _body_mass_g_ vs _flipper_length_mm_, colored by _bill_depth_mm_, with a smooth curve.

```r
ggplot(penguins, aes(x = flipper_length_mm, y = body_mass_g)) +
  geom_point(aes(color = bill_depth_mm), size = 2, alpha = 0.8) +
  geom_smooth(se = TRUE) +
  labs(
    title = "Body Mass vs. Flipper Length",
    x     = "Flipper Length (mm)",
    y     = "Body Mass (g)",
    color = "Bill Depth (mm)",
    caption = "Data come from the palmerpenguins package."
  )
```

- **Aesthetic mapping**:
    
    - `bill_depth_mm` → **color**, at the **`geom_point()`** level (so the smooth line isn’t colored).
        

---

### 9. Predict the output of:

```r
ggplot(
  data = penguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g, color = island)
) +
  geom_point() +
  geom_smooth(se = FALSE)
```

- **Prediction**:
    
    - Points colored by `island`.
        
    - One smooth curve **per island** (because the color grouping is inherited), no confidence band.
        

---

### 10. Will these two graphs look different?

```r
# A
ggplot(
  data = penguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g)
) +
  geom_point() +
  geom_smooth()

# B
ggplot() +
  geom_point(
    data = penguins,
    mapping = aes(x = flipper_length_mm, y = body_mass_g)
  ) +
  geom_smooth(
    data = penguins,
    mapping = aes(x = flipper_length_mm, y = body_mass_g)
  )
```

- **Answer**: No—they’ll be identical.
    
    - In A, you set `data` and `aes` globally.
        
    - In B, you repeat them in each layer.
        
    - Result: same points + same smooth line with CI.
        

---

## ✅ Key Takeaways

- Always check your **axis labels** match your `aes(x, y)`.
    
- Use **boxplots** or **violins** when plotting a continuous against a categorical variable.
    
- Remember to supply **`aes(x, y)`** or you’ll get an error.
    
- **`na.rm = TRUE`** quietly drops missing values.
    
- **Captions** live in `labs(caption = "...")`.
    
- Map continuous color scales at the **geom** level if you don’t want the grouping applied to other geoms.
    
- **Global vs. per-layer** `data`/`aes` is purely syntactic—plots only care about the final mapping.

## 1.3 ggplot2 calls