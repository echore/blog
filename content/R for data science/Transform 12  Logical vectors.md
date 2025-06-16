---
share: true
date: 2025-06-16
---
## 12.2 Comparisons

#### How does `filter()` use logical vectors?

- `filter()` takes these TRUE/FALSE values and **keeps only the rows where the condition is TRUE**.
    
- So, when you write:
    
    ```r
    flights |> 
      filter(dep_time > 600 & dep_time < 2000 & abs(arr_delay) < 20)
    ```
    
    You’re saying:
    
    - Keep flights that left **during the day** (6:01 AM to 7:59 PM),
        
    - **AND** arrived within 20 minutes of the scheduled time (either early or late).
        
- **Shortcut:** You can put the logic right inside `filter()`.
    
- **But:** This logic is “invisible”—it’s used once and then discarded.
    

---

#### Why Use `mutate()` to Create Logical Variables?

With `mutate()`, you **name** your logical variables and make them visible in your data.

```r
flights |> 
  mutate(
    daytime = dep_time > 600 & dep_time < 2000,
    approx_ontime = abs(arr_delay) < 20,
    .keep = "used"
  )
```

- `daytime`: TRUE if flight left during the day.
    
- `approx_ontime`: TRUE if flight arrived within 20 minutes of scheduled time.
    

Now, every row will have these new columns:

- Easy to check: Did you get the logic right?
    
- Easy to reuse: No need to repeat the logic.
    

---

#### What does `.keep = "used"` do in `mutate()`?

- By default, when you use `mutate()`, it keeps **all the columns** in your data, plus any new columns you create.
    
- Sometimes, especially when you’re creating a lot of temporary variables, you might want to **control** which columns remain in your resulting data.
    

`.keep = "used"` means:

> **After the mutate, only keep the columns that were used to create the new variables, plus the new variables themselves.**


**Other `.keep` Options**

- `.keep = "all"` (default): Keep **all** columns (old and new).
    
- `.keep = "used"`: Keep only columns **used** to compute the new columns, plus the new columns.
    
- `.keep = "unused"`: Keep only columns **not used** to compute the new columns, plus the new columns.
    
- `.keep = "none"`: Only the **new columns** remain.
    
    


---

#### Why is This Useful?

- **Clarity:** Naming logic makes your code easier to understand (“self-documenting”).
    
- **Debugging:** You can check if your logic works as expected.
    
- **Complexity:** For multi-step logic, breaking it up with named columns avoids mistakes and confusion.
    

---

#### Equivalent Code, More Readable

Compare:

```r
flights |> 
  filter(dep_time > 600 & dep_time < 2000 & abs(arr_delay) < 20)
```

vs.

```r
flights |> 
  mutate(
    daytime = dep_time > 600 & dep_time < 2000,
    approx_ontime = abs(arr_delay) < 20
  ) |>
  filter(daytime & approx_ontime)
```

**Result is the same, but the second version is easier to read, check, and extend.**

---

### 12.2.1 Floating point comparison

Beware of using `==` with numbers. For example, it looks like this vector contains the numbers 1 and 2:

```
x <- c(1 / 49 * 49, sqrt(2) ^ 2)
x
#> [1] 1 2
```

But if you test them for equality, you get `FALSE`:

```
x == c(1, 2)
#> [1] FALSE FALSE
```

What’s going on? Computers store numbers with a fixed number of decimal places so there’s no way to exactly represent 1/49 or `sqrt(2)` and subsequent computations will be very slightly off. We can see the exact values by calling `[print()` with the `digits` argument:

```
print(x, digits = 16)
#> [1] 0.9999999999999999 2.0000000000000004
```
You can see why R defaults to rounding these numbers; they really are very close to what you expect.

Now that you’ve seen why `==` is failing, what can you do about it? One option is to use `dplyr::near()`which ignores small differences:

```
near(x, c(1, 2))
#> [1] TRUE TRUE
```

---

### 12.2.2 Missing values

Missing values represent the unknown so they are “contagious”: almost any operation involving an unknown value will also be unknown:

```
NA > 5
#> [1] NA
10 == NA
#> [1] NA
```

The most confusing result is this one:

```
NA == NA
#> [1] NA
```

It’s easiest to understand why this is true if we artificially supply a little more context:
```r
# We don't know how old Mary is
age_mary <- NA

# We don't know how old John is
age_john <- NA

# Are Mary and John the same age?
age_mary == age_john
#> [1] NA
# We don't know!
```

So if you want to find all flights where `dep_time` is missing, the following code doesn’t work because `dep_time == NA` will yield `NA` for every single row, and `filter()` automatically drops missing values:

``` r
flights |> 
  filter(dep_time == NA)
#> # A tibble: 0 × 19
#> # ℹ 19 variables: year <int>, month <int>, day <int>, dep_time <int>,
#> #   sched_dep_time <int>, dep_delay <dbl>, arr_time <int>, …
```

Instead we’ll need a new tool: `is.na()`.

---
### 12.2.3 `is.na()`
`is.na(x)` works with any type of vector and returns `TRUE` for missing values and `FALSE` for everything else

We can use `is.na()` to find all the rows with a missing `dep_time`:
```r
flights |> 
  filter(is.na(dep_time))
#> # A tibble: 8,255 × 19
#>    year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
#>   <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
#> 1  2013     1     1       NA           1630        NA       NA           1815
#> 2  2013     1     1       NA           1935        NA       NA           2240
#> 3  2013     1     1       NA           1500        NA       NA           1825
#> 4  2013     1     1       NA            600        NA       NA            901
#> 5  2013     1     2       NA           1540        NA       NA           1747
#> 6  2013     1     2       NA           1620        NA       NA           1746
#> # ℹ 8,249 more rows
#> # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>, …
```
`is.na()`  can also be useful in `arrange()`.  `arrange()` usually puts all the missing values at the end but you can override this default by first sorting by `is.na()`


```r
flights %>% 
  filter(
    month == 1,day == 1
  ) %>% 
  arrange(desc(is.na(dep_time)))
```

- `is.na(dep_time)` returns **TRUE** if `dep_time` is missing, **FALSE** otherwise.
    
- `desc(is.na(dep_time))` puts all the rows where `dep_time` is **NA** (missing) **first** (since `desc(TRUE)` > `desc(FALSE)`).
    
- **No further sorting**—within those groups, the order is arbitrary.
    

**Second Code:**

```r
flights %>% 
  filter(
    month == 1,day == 1
  ) %>% 
  arrange(desc(is.na(dep_time)),dep_time)
```

- This also puts all missing `dep_time` rows **first**.
    
- **But**: Within each group (missing or not missing), it further **sorts by `dep_time`** (from lowest to highest, because default is ascending).
    
- So for non-missing `dep_time` values, you get a **chronological order**.
    
 **In Simple Terms:**

|Code|Sorting Priority|
|---|---|
|`arrange(desc(is.na(dep_time)))`|1. Missing first (order within each group = random)|
|`arrange(desc(is.na(dep_time)), dep_time)`|1. Missing first 2. If not missing, sort by time (earliest to latest)|

---
### 12.2.4 Exercises
Use `mutate(), is.na(), and count()` together to describe how the missing values in `dep_time, sched_dep_time and dep_delay` are connected

It's asking you to **explore** and **summarize** how the missing values in `dep_time`, `sched_dep_time`, and `dep_delay` are related.  
For example: _If a row is missing `dep_time`, is it also missing the other two? Are the missingness patterns always the same, or do they differ?_

```r
> flights %>% 
+   mutate(
+     miss_dep_time = is.na(dep_time),
+     miss_sched_dep_time = is.na(sched_dep_time),
+     miss_dep_delay = is.na(dep_delay)
+   ) %>% 
+   count(miss_dep_time,miss_sched_dep_time,miss_dep_delay)
# A tibble: 2 × 4
  miss_dep_time miss_sched_dep_time miss_dep_delay      n
  <lgl>         <lgl>               <lgl>           <int>
1 FALSE         FALSE               FALSE          328521
2 TRUE          FALSE               TRUE             8255
```
- `miss_dep_time == TRUE`: `dep_time` **is** missing
    
- `miss_sched_dep_time == FALSE`: `sched_dep_time` is **not** missing
    
- `miss_dep_delay == TRUE`: `dep_delay` **is** missing
    
- **n = 8,255:** There are 8,255 flights where both the actual departure time (`dep_time`) **and** the departure delay (`dep_delay`) are missing, but the scheduled departure time (`sched_dep_time`) is **present**.

 **How are the Missing Values Connected?**

- **Whenever `dep_time` is missing, `dep_delay` is also missing.**  
    (You never see a row where one is missing and the other isn’t.)
    
- **`sched_dep_time` is never missing** (always FALSE for this variable), no matter what happens to the other two.
    
- **Most rows** (the vast majority) have no missing values at all.

---
## 12.3 Boolean algebra
