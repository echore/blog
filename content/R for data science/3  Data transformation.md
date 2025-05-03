---
share: true
date: 2025-04-30
---
### 3.1.1 Prerequisites

`flights` is a tibble, a special type of data frame used by the tidyverse to avoid some common gotchas. The most important difference between tibbles and data frames is the way tibbles print; they are designed for large datasets, so they only show the first few rows and only the columns that fit on one screen. There are a few options to see everything. If you’re using RStudio, the most convenient is probably `View(flights)`, which opens an interactive, scrollable, and filterable view. Otherwise you can use `print(flights, width = Inf)` to show all columns, or use `glimpse()`

### 3.1.3 dplyr basics

You’re about to learn the primary dplyr verbs (functions), which will allow you to solve the vast majority of your data manipulation challenges. But before we discuss their individual differences, it’s worth stating what they have in common:

1. The first argument is always a data frame.
    
2. The subsequent arguments typically describe which columns to operate on using the variable names (without quotes).
    
3. The output is always a new data frame.

```r
flights %>% 
  filter(dest == 'IAH') %>% 
  group_by(year, month, day) %>% 
  summarise(
    arr_delay = mean(arr_delay, na.rm = TRUE)
  )
```

dplyr’s verbs are organized into four groups based on what they operate on: **rows**, **columns**, **groups**, or **tables**.

## 3.2 Rows
### 3.2.1 `filter()`

`filter()` allows you to keep rows based on the values of the columns. The first argument is the data frame. The second and subsequent arguments are the conditions that must be true to keep the row.

```r
flights %>% 
  filter(dep_delay > 120)

flights %>% 
  filter(month == 1 & day == 1 )
```

There’s a useful shortcut when you’re combining `|` and `==`: `%in%`

🌟 A simple analogy:

Think of `%in%` as asking:

> "Is this student on the attendance list?"

instead of checking:

> "Is it Alice OR Bob OR Charlie OR David...?" one by one.

```r
flights %>% 
  filter(month %in% c(1,2,3))
```

When you run `filter()` dplyr executes the filtering operation, creating a new data frame, and then prints it. It doesn’t modify the existing `flights` dataset because dplyr functions never modify their inputs. To save the result, you need to use the assignment operator, `<-`:
```r
jan <- flights %>% 
  filter(month == 1)
```


### 3.2.2 Common mistakes

When you’re starting out with R, the easiest mistake to make is to use `=` instead of `==` when testing for equality

### 3.2.3 `arrange()`

`arrange()` changes the order of the rows based on the value of the columns. It takes a data frame and a set of column names (or more complicated expressions) to order by. If you provide more than one column name, each additional column will be used to break ties in the values of the preceding columns.

You can use `desc()` on a column inside of `arrange()` to re-order the data frame based on that column in descending (big-to-small) order.

```r
flights %>% 
  arrange(desc(dep_delay))
```

### 3.2.4 `distinct()`
`distinct()` finds all the unique rows in a dataset, so technically, it primarily operates on the rows.
Alternatively, if you want to keep the other columns when filtering for unique rows, you can use the `.keep_all = TRUE` option.

```r
flights %>% 
  distinct(origin,dest, .keep_all = TRUE)
```

If you want to find the number of occurrences instead, you’re better off swapping `distinct()` for `count()`. With the `sort = TRUE` argument, you can arrange them in descending order of the number of occurrences.
```r
flights %>% 
  count(origin,dest,sort = TRUE)
```

### 3.2.5 Exercises

1. Sort `flights` to find the flights with the longest departure delays. Find the flights that left earliest in the morning.
	**Among the most delayed flights**, show the ones that left earliest

```r
flights %>% 
  arrange(desc(dep_delay),sched_dep_time) %>% 
  relocate(dep_delay,sched_dep_time)
```

In dplyr, multiple uses of arrange() will overwrite the previous sorting. If you want to "sort by B after sorting A", you should combine them into one line:
`arrange(A, B) # instead of arrange(A) |> arrange(B)`

❓ Why use `sched_dep_time` instead of `dep_time`?

1. **`sched_dep_time` = Scheduled time** → always exists ✅

2. **`dep_time` = Actual time** → often missing ❌ (if the flight was canceled)

📊 For analysis:

We use `sched_dep_time` to:

- Compare **planned schedules**
- Analyze **what time flights were _supposed_ to leave**, even if they were delayed or canceled

We use `dep_time` only when we care about **actual operations**, but many rows are missing.

Example:

If you're looking for **delayed morning flights**, use `dep_delay` + `sched_dep_time`.  
If you use `dep_time`, you might accidentally include `NA` (canceled) or get misleading times.

---

2. Sort `flights` to find the fastest flights. (Hint: Try including a math calculation inside of your function.)
```r
flights %>% 
  mutate(speed=distance / (air_time / 60)) %>% 
  arrange(desc(speed)) %>% 
  relocate(speed)
```
❓ Why add `relocate(speed)`?

It does **not affect your data**, it just:

- Moves the new `speed` column to the **front of the table**
    
- Makes it **easier for your eyes** to quickly see the variable you just created
    

Otherwise, `speed` would appear at the **very end**, especially annoying in a wide dataset like `flights` (which has over 15 columns).

---

3. Was there a flight on every day of 2013?
	Check if there was **at least one flight per day in 2013**.
```r
flights %>% 
  distinct(year,month,day) %>%  #I don’t care about which flights — just show me one row per day ,you have a list of days when at least one flight happened. 
  nrow() #It counts how many days are in that list. If 365 then at least one flight per day in 2013
```

## 3.3 Columns

### 3.3.1 `mutate()`

The job of `mutate()` is to add new columns that are calculated from the existing columns.
By default, `mutate()` adds new columns on the right-hand side of your dataset, which makes it difficult to see what’s happening here. We can use the `.before` argument to instead add the variables to the left-hand side
```r
flights %>% 
  mutate(
    gain = dep_delay - arr_delay,
    speed = distance / arr_time * 60,
    .before = 1
  )
```

You can also use `.after` to add after a variable, and in both `.before` and `.after` you can use the variable name instead of a position. For example, we could add the new variables after `day`:
```r
flights %>% 
  mutate(
    gain = dep_delay - arr_delay,
    speed = distance / arr_time * 60,
    .after = day
  )
```

Alternatively, you can control which variables are kept with the `.keep` argument. A particularly useful argument is `"used"` which specifies that we only keep the columns that were involved or created in the `mutate()` step.
```r
flights %>% 
  mutate(
    gain = dep_delay - arr_delay,
    speed = distance / arr_time * 60,
    .after = day,
    .keep = 'used'
  )
```

### 3.3.2 `select()`

- Select columns by name:
    
    ```r
    flights %>% 
	    select(year,month,day)
    ```
    
- Select all columns between year and day (inclusive):
    
    ```r
    flights %>% 
      select(year:day)
    ```
    
- Select all columns except those from year to day (inclusive):
    
    ```r
    flights %>%  
      select(!year:day)
    ```
    
    Historically this operation was done with `-` instead of `!`, so you’re likely to see that in the wild. These two operators serve the same purpose but with subtle differences in behavior. We recommend using `!` because it reads as “not” and combines well with `&` and `|`.
    
- Select all columns that are characters:
    
    ```r
    flights %>% 
      select(where(is.character))
    ```
    

There are a number of helper functions you can use within `select():

- `starts_with("abc")`: matches names that begin with “abc”.
- `ends_with("xyz")`: matches names that end with “xyz”.
- `contains("ijk")`: matches names that contain “ijk”.
- `num_range("x", 1:3)`: matches `x1`, `x2` and `x3`.

See `?select` for more details. 
```r
flights %>% 
  select(contains("time"))
```

You can rename variables as you `select()` them by using `=`. The new name appears on the left-hand side of the `=`, and the old variable appears on the right-hand side:
```r
flights %>% 
  select(tail_num=tailnum)
```

### 3.3.3 `rename()`
If you want to keep all the existing variables and just want to rename a few, you can use `rename()` instead of `select()

### 3.3.4 `relocate()`

Use `relocate()` to move variables around. You might want to collect related variables together or move important variables to the front. By default `relocate` to move variables to the front
```r
flights %>% 
  relocate(year:dep_time,
           .after=day)

flights %>% 
  relocate(starts_with('arr'),.before = day)
```

### 3.3.5 Exercises
1. What does the `any_of()` function do? Why might it be helpful in conjunction with this vector?
    
 ```
    variables <- c("year", "month", "day", "dep_delay", "arr_delay")
```
You ask if `any_of()` these variables have a certain thing you are looking for.
```r
variables <- c("year", "month", "day", "dep_delay", "arr_delay")

flights %>% 
  select(any_of(variables))
```

## 3.5 Groups
### 3.5.1 `group_by()`

```r
flights %>% 
  group_by(month)
```
`group_by()` doesn’t change the data but, if you look closely at the output, you’ll notice that the output indicates that it is “grouped by” month

### 3.5.2 `summarize()`
one very useful summary is `n()`, which returns the number of rows in each group:
```r
flights %>% 
  group_by(month) %>% 
  summarise(avg_delay = mean(dep_delay,na.rm = TRUE),
            n = n())
```

### 3.5.3 The `slice_` functions
There are five handy functions that allow you to extract specific rows within each group:

- `df |> slice_head(n = 1)` takes the first row from each group.
- `df |> slice_tail(n = 1)` takes the last row in each group.
- `df |> slice_min(x, n = 1)` takes the row with the smallest value of column `x`.
- `df |> slice_max(x, n = 1)` takes the row with the largest value of column `x`.
- `df |> slice_sample(n = 1)` takes one random row.

You can vary `n` to select more than one row, or instead of `n =`, you can use `prop = 0.1` to select (e.g.) 10% of the rows in each group. For example, the following code finds the flights that are most delayed upon arrival at each destination:
```r
flights %>% 
  group_by(dest) %>% 
  slice_max(arr_delay,n=1) %>% 
  relocate(dest,arr_delay)
```

why 108 rows for 105 destinations?

Because of **tied values** — multiple rows **within a group** (i.e., within the same `dest`) can **share the same maximum `arr_delay`**.

### 3.5.5 Ungrouping
what happens when you summarize an ungrouped data frame:
You get a single row back because dplyr treats all the rows in an ungrouped data frame as belonging to one group.

### 3.5.6 `.by`

dplyr 1.1.0 includes a new, experimental, syntax for per-operation grouping, the `.by` argument. `group_by()` and `ungroup()` aren’t going away, but you can now also use the `.by` argument to group within a single operation:
```r
flights %>% 
  summarise(
    delay = mean(dep_delay,na.rm=TRUE),
    n = n(),
    .by = month
  )
```

### 3.5.7 Exercises

1. Which carrier has the worst average delays?
```r
flights %>% 
  group_by(carrier) %>% 
  summarise(
    delay = mean(dep_delay,na.rm=TRUE),
  ) %>% 
  arrange(desc(delay))
```

2.  Find the flights that are most delayed upon departure from each destination.
```r
flights %>%
  group_by(dest) %>%
  slice_max(dep_delay, n = 1) %>%
  relocate(dest)
```

3.  How do delays vary over the course of the day? Illustrate your answer with a plot.
```r
flights %>% 
  group_by(hour) %>% 
  summarise(avg_depdelay = mean(dep_delay,na.rm = TRUE)) %>% 
  ggplot(aes(x = hour,y = avg_depdelay)) +
  geom_smooth()
```

4. Explain what count() does in terms of the dplyr verbs you just learned. What does the sort argument to count() do?
🔧 What `count()` Does

The `count()` function is actually a **shortcut** for a combination of `group_by()` + `summarise(n = n())`:

```r
df %>% 
  group_by(variable) %>% 
  summarise(n = n())
```

So this:

```r
count(df, variable)
```

is equivalent to:

```r
df %>% 
  group_by(variable) %>% 
  summarise(n = n())
```

It counts how many rows fall into each unique value of `variable`.

 🧹 What `sort = TRUE` Does

By default, `count()` returns the results in **the order that the groups appear** in the data. But when you add `sort = TRUE`, it **automatically arranges the output from the most common group to the least** — that is, it sorts the result by `n` in descending order:

```r
count(df, variable, sort = TRUE)
```

is like doing:

```r
df %>% 
  group_by(variable) %>% 
  summarise(n = n()) %>%
  arrange(desc(n))
```

---

✅ Example

```r
flights %>% count(dest, sort = TRUE)
```

→ Tells you **which destinations had the most flights**, sorted from most to least.
