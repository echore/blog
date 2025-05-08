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

## 7.3 Controlling column types
### 7.3.2 Missing values, column types, and problems

The most common way column detection fails is that a column contains unexpected values, and you get a character column instead of a more specific type. One of the most common causes for this is a missing value, recorded using something other than the `NA` that readr expects.
```r
simple_csv <- "
  x
  10
  .
  20
  30"

df <- read_csv(simple_csv,col_types = cols(x = col_double())) #This forces R to try to read `x` as **double** (numeric with decimals).
problems(df) 
> problems(df)
# A tibble: 1 × 5
    row   col expected actual file                                                                  
  <int> <int> <chr>    <chr>  <chr>                                                                 
1     3     1 a double .      
#This tells us that there was a problem in row 3, col 1 where readr expected a double but got a `.`. That suggests this dataset uses `.`
df <- read_csv(simple_csv,na = '.')
df
```
In this very small case, you can easily see the missing value `.`. But what happens if you have thousands of rows with only a few missing values represented by `.`s sprinkled among them? One approach is to tell readr that `x` is a numeric column, and then see where it fails.

### 7.3.3 Column types
By default, `read_csv()` **guesses** column types. But sometimes you want:

- **all columns** to be one type (e.g. character),
    
- or to **override just a few**, leaving others default.
```r
another_csv <- "
x,y,z
1,2,3"

read_csv(another_csv,col_types = cols(.default = col_character()))
# A tibble: 1 × 3                                                                                   
  x     y     z    
  <chr> <chr> <chr>
1 1     2     3    
```
This tells R: Treat **all columns** as characters unless I say otherwise.
This is super useful when:

- You're importing **dirty or inconsistent data**
    
- You want to **avoid auto-parsing errors** (e.g. converting ZIP codes like `"01234"` to numbers)
    
- You’re working with **IDs or codes** that look numeric but should stay as strings

Another useful helper is `cols_only()` which will read in only the columns you specify:
```r
read_csv(another_csv,col_types = cols_only(x = col_character()))
# A tibble: 1 × 1                                                                                   
  x    
  <chr>
1 1 
```
`cols_only(): `**Only read in the columns you specify.**  All other columns are ignored entirely — they don’t even appear in the output.

How Is It Different from `select()`?

- `select()` drops columns _after_ the file has been read (i.e., after parsing all columns).
    
- `cols_only()` **prevents them from being read** in the first place — more efficient.

## 7.4 Reading data from multiple files
```r
sales_files <- c(
  "https://pos.it/r4ds-01-sales",
  "https://pos.it/r4ds-02-sales",
  "https://pos.it/r4ds-03-sales"
)
read_csv(sales_files, id = "file")
```
What Does `id = "file"` Do?

It tells `read_csv()` to:

1. **Add a new column** to your final tibble called `"file"`.
    
2. **Fill it with the file path** (or name) from which each row came.
    

This is **super helpful** when you want to:

- Keep track of **data source** per row,
    
- Later do **grouped summaries** by file (e.g., total sales per month),
    
- Debug or trace back **inconsistencies** to specific files.

---

## 7.5 Writing to a file

### CSV vs RDS vs Parquet in R

#### 1. `write_csv()` / `read_csv()`

**Best for:** Portability & sharing with others  
**File type:** Plain text (CSV)

Pros:

- Human-readable
    
- Works across Excel, Python, etc.
    
- Easy to share via email or version control
    
 Cons:

- Loses column type info (e.g., factors → characters)
    
- Must re-specify types (`col_types`) each time
    
- Slower for large data
    

```r
write_csv(students, "students.csv")
students2 <- read_csv("students.csv")
```

---

#### 2. `write_rds()` / `read_rds()`

**Best for:** Fast internal caching of R objects  
**File type:** Binary (.rds)

Pros:

- Preserves all types (factors, dates, lists)
    
- Fast read/write
    
- Compact
    
 Cons:

- R-specific (not readable outside R)
    
- Not human-readable
    

```r
write_rds(students, "students.rds")
students3 <- read_rds("students.rds")
```

---

#### 3. `write_parquet()` / `read_parquet()` (via `arrow`)

**Best for:** High-performance cross-platform analytics  
**File type:** Binary (Parquet)

Pros:

- Retains full type info
    
- Cross-language support (Python, Spark, SQL, etc.)
    
- Highly compressed and fast
    
- Columnar format: ideal for big data
    
 Cons:

- Requires `arrow` package
    
- Not human-readable
    

```r
library(arrow)
write_parquet(students, "students.parquet")
students4 <- read_parquet("students.parquet")
```

---
## 7.6 Data entry

Sometimes, you don’t want to read from a file — you just want to **manually create a small dataset** (for testing, examples, teaching, etc.).

Two helper functions for this:

|Function|Layout style|Best for|
|---|---|---|
|`tibble()`|Column-wise|Programmers/data gen|
|`tribble()`|Row-wise|Humans/data entry|

`tibble()` — Column-Wise Data Entry

```r
tibble(
  x = c(1, 2, 5), 
  y = c("h", "m", "g"),
  z = c(0.08, 0.83, 0.60)
)
#> # A tibble: 3 × 3
#>       x y         z
#>   <dbl> <chr> <dbl>
#> 1     1 h      0.08
#> 2     2 m      0.83
#> 3     5 g      0.6
```

The result is a table with 3 rows and 3 columns.  
But you have to **mentally line up the values across columns** to see each row.

> Think of `tibble()` like defining **columns in a spreadsheet** first — one column at a time.


`tribble()` — Row-Wise Data Entry

```r
tribble(
  ~x, ~y, ~z,
  1, "h", 0.08,
  2, "m", 0.83,
  5, "g", 0.60
)
#> # A tibble: 3 × 3
#>       x y         z
#>   <dbl> <chr> <dbl>
#> 1     1 h      0.08
#> 2     2 m      0.83
#> 3     5 g      0.6
```

This says:

- First row: `x = 1`, `y = "h"`, `z = 0.08`
    
- Second row: `x = 2`, `y = "m"`, `z = 0.83`
    
- ...

Each row is laid out **visually and structurally as a row**, making it easier to read and maintain for small tables.

