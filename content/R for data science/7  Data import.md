---
share: true
date: 2025-05-07
---
### 7.2.1 Practical advice
```r
library(tidyverse)
students <- read_csv("https://pos.it/r4ds-students-csv",na=c('N/A',''))
```
In the `favourite.food` column, there are a bunch of food items, and then the character string `N/A`, which should have been a real `NA` that R will recognize as “not available”. This is something we can address using the `na` argument. By default, `read_csv()` only recognizes empty strings (`""`) in this dataset as `NA`s, and we want it to also recognize the character string `"N/A"`
```r
students
#> # A tibble: 6 × 5
#>   `Student ID` `Full Name`      favourite.food     mealPlan            AGE  
#>          <dbl> <chr>            <chr>              <chr>               <chr>
#> 1            1 Sunil Huffmann   Strawberry yoghurt Lunch only          4    
#> 2            2 Barclay Lynn     French fries       Lunch only          5    
#> 3            3 Jayendra Lyne    N/A                Breakfast and lunch 7    
#> 4            4 Leon Rossini     Anchovies          Lunch only          <NA> 
#> 5            5 Chidiegwu Dunkel Pizza              Breakfast and lunch five 
#> 6            6 Güvenç Attila    Ice cream          Lunch only          6
```

You might also notice that the `Student ID` and `Full Name` columns are surrounded by backticks. That’s because they contain spaces, breaking R’s usual rules for variable names; they’re **non-syntactic** names. To refer to these variables, you need to surround them with backticks
```r
students %>% 
  rename(
    student_id = `Student ID`,
    full_name = `Full Name`
  )
```
An alternative approach is to use `janitor::clean_names()` to use some heuristics to turn them all into snake case at once
```r
library(janitor)
students %>% 
  janitor::clean_names()
```
What does `janitor::clean_names()` do?

It **standardizes column names** in a data frame by:

- Removing special characters
    
- Replacing spaces with underscores
    
- Converting names to lowercase
    
- Making them syntactically valid R variable names
like automatic way to standardizes column names.
---

Another common task after reading in data is to consider variable types. For example, `meal_plan` is a categorical variable with a known set of possible values, which in R should be represented as a factor:

```r
students %>% 
  janitor::clean_names() %>% 
  mutate(
    meal_plan = factor(meal_plan)
  )
```
What is a factor in R?

A **factor** is a special data type in R used to represent **categorical variables**, especially those with a **fixed and known set of possible values**, like:

- `"Lunch only"`
    
- `"Breakfast and lunch"`
    
- `"None"`
    

These are _not just strings_ (characters) — they are categories, and that distinction matters.

---

Before you analyze these data, you’ll probably want to fix the `age` column. Currently, `age` is a character variable because one of the observations is typed out as `five` instead of a numeric `5`
```r
students %>% 
  janitor::clean_names() %>% 
  mutate(
    meal_plan = factor(meal_plan),
    age = parse_number(if_else(age == 'five','5',age))
  )
```

### 7.2.2 Other arguments
When you use `readr::read_csv()` in R, it assumes that the first line of your CSV file contains column names. But sometimes, the first few lines aren’t actual data

`read_csv("students.csv", skip = 3)`

> ⏩ Skips the first 3 lines — great when you know exactly how many metadata lines to ignore.

Now R will correctly read the 4th line as column headers, and the rest as data.

`read_csv("students.csv", comment = "#")`

> 🧹 This tells R: “Ignore any line that starts with #.”

It’s perfect for files that mix metadata and data, as long as metadata lines all start with `#`.

This is more flexible and robust, especially when the number of comment lines can change.

---
In other cases, the data might not have column names. You can use `col_names = FALSE` to tell `read_csv()` not to treat the first row as headings and instead label them sequentially from `X1` to `Xn`:
```r
read_csv(
  "1,2,3
  4,5,6",
  col_names = FALSE
)
```
Alternatively, you can pass `col_names` a character vector which will be used as the column names:
```r
read_csv(
  "1,2,3
  4,5,6",
  col_names = c('x','y','z')
)
```

### 7.2.4 Exercises
Sometimes strings in a CSV file contain commas. To prevent them from causing problems, they need to be surrounded by a quoting character, like `"` or `'`. By default, `read_csv()` assumes that the quoting character will be `"`. To read the following text into a data frame, what argument to `read_csv()` do you need to specify?

```
"x,y\n1,'a,b'"
```

```r
read_csv("x,y\n1,'a,b'", quote = "'")
```

What is `quote` in `read_csv()`?

In a **CSV (Comma-Separated Values)** file, sometimes a value contains a comma **inside the data** (not between columns). To make sure it’s treated as a **single value**, we wrap it in quotes — this is where the `quote` character comes in.

```csv
name,favorite_food
Alice,"pizza, extra cheese"
```

In this example:

- There are **two columns**
    
- The second value in the second row is `"pizza, extra cheese"` → not two columns, but **one string**
    

👉 The **quote character** tells the parser:

> “Everything inside me is one value — don’t split it even if there’s a comma!”


 Default behavior in `read_csv()`

- `read_csv()` assumes that the **quote character is `"`** (double quote).
    
- This works for most files.
    

```r
read_csv("name,food\nAlice,\"pizza, extra cheese\"")
```

✅ Correctly reads two columns: `"Alice"` and `"pizza, extra cheese"`


How to change the quote character

If your file uses **single quotes (`'`)** instead of double quotes (`"`) to wrap text, you need to tell R:

```r
read_csv("x,y\n1,'a,b'", quote = "'")
```

Otherwise, R doesn’t know that `'a,b'` is one value, and it will wrongly split it into two columns.

---
Practice referring to non-syntactic names in the following data frame by:

1. Extracting the variable called `1`.
2. Plotting a scatterplot of `1` vs. `2`.
3. Creating a new column called `3`, which is `2` divided by `1`.
4. Renaming the columns to `one`, `two`, and `three`.

```
annoying <- tibble(
  `1` = 1:10,
  `2` = `1` * 2 + rnorm(length(`1`))
)
```

```r
annoying %>% 
  select(`1`) # non-syntactic names so we use ``
# Better Solution: Rename them! but this question doesn't mean that.

ggplot(annoying, aes(x = `2`, y = `1`)) + 
# Backticks tell R: "This is a column name, not a number"
  geom_point()

annoying %>% 
  mutate(
    `3` = `2` / `1`
  ) %>% 
  rename(
    'one' = `1`,
    "two" = `2`,
    "three" = `3`
  )
```
