---
share: true
date: 2025-05-03
---

> _Good code style is like good punctuation: not required, but essential for readability and collaboration._

---

### 🔤 4.1 Variable Naming

- Use **lowercase**, **underscores `_`**, and **clear, descriptive names**
    
- ✅ `short_flights <- flights |> filter(air_time < 60)`
    
- ❌ `SHORTFLIGHTS <- flights |> filter(air_time < 60)`
    
- Prefer **prefixes** (helps with autocompletion)
    

---

### ␣ 4.2 Spaces

- Add spaces around `+`, `-`, `==`, `<`, and `<-` (but not `^`)
    
- No spaces around parentheses in function calls
    
- Use spaces after commas
    
- Align `=` in `mutate()` or similar for readability:
    

```r
flights |> 
  mutate(
    speed      = distance / air_time,
    dep_hour   = dep_time %/% 100,
    dep_minute = dep_time %%  100
  )
```

---

### 🔗 4.3 Pipes `|>`

- Always have a space before `|>` and place at end of line
    
- Chain each verb on its own line
    
- Indent each step by 2 spaces
    
- For named arguments, put each on its own line
    
- Keep pipelines short (split and name intermediate steps if too long)
    

```r
flights |>  
  group_by(tailnum) |> 
  summarize(
    delay = mean(arr_delay, na.rm = TRUE),
    n = n()
  )
```

---

### 📈 4.4 `ggplot2` Formatting

- Use `+` like `|>` (space before, at end of line)
    
- Long argument lists → one per line
    
- Indent consistently
    

```r
ggplot(data, aes(x, y)) +
  geom_point() +
  geom_smooth(
    method = "loess",
    span = 0.5,
    se = FALSE
  )
```

---

### 🧩 4.5 Sectioning Comments

Use headers to organize long scripts:

```r
# Load data -------------------------------------------------

# Clean data ------------------------------------------------

# Visualize -------------------------------------------------
```

Shortcut in RStudio: `Cmd/Ctrl + Shift + R`

---

### 🛠 Tools

- Use the `{styler}` package to auto-format code:
- Use via RStudio’s command palette (`Cmd/Ctrl + Shift + P` → "styler")
- **quite useful**

---

### 📌 4.7 Summary

- A consistent style improves collaboration and future debugging.
    
- Follow tidyverse conventions for naming, spacing, and pipes.
    
- Use `styler` to clean up messy code. 
