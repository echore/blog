---
share: true
date: 2025-05-09
---
## 8.1 Google is your friend
If you get stuck, start with Google. Typically adding “R” to a query is enough to restrict it to relevant results: if the search isn’t useful, it often means that there aren’t any R-specific results available. 
Additionally, adding package names like “tidyverse” or “ggplot2” will help narrow down the results to code that will feel more familiar to you as well, e.g., “how to make a boxplot in R” vs. “how to make a boxplot in R with ggplot2”. 
Google is particularly useful for error messages. If you get an error message and you have no idea what it means, try googling it!

## 8.2 Making a reprex
If your googling doesn’t find anything useful, it’s a really good idea to prepare a **reprex,** short for minimal **repr**oducible **ex**ample.There are two parts to creating a reprex:

- First, you need to make your code reproducible. This means that you need to capture everything, i.e. include any `library()` calls and create all necessary objects. The easiest way to make sure you’ve done this is using the reprex package.

- Second, you need to make it minimal. Strip away everything that is not directly related to your problem. This usually involves creating a much smaller and simpler R object than the one you’re facing in real life or even using built-in data.
copy-paste and run `reprex()`

**Step by step:**

1. Highlight the code **you want to test**
    
2. **Copy it** to your clipboard (Ctrl+C or Cmd+C)
    
3. In the R console, just run
    
    `reprex::reprex()`

`reprex()` now runs your copied code in a **fresh R session**, captures the output, and formats it.

There are three things you need to include to make your example reproducible: required packages, data, and code.

1. **Packages** should be loaded at the top of the script so it’s easy to see which ones the example needs. This is a good time to check that you’re using the latest version of each package; you may have discovered a bug that’s been fixed since you installed or last updated the package. For packages in the tidyverse, the easiest way to check is to run `tidyverse_update()`.
    
2. The easiest way to include **data** is to use `dput()`

What is `dput()` really doing?

`dput()` **converts an R object into text code** that, when pasted somewhere else, **recreates the exact same object**.

Step-by-step example: Use `dput()` to share data in a reprex

🔹 Step 1: Start with a small piece of your data

Let’s say you have a dataframe `df` like this:

```r
df <- tibble(
  name = c("Alice", "Bob"),
  score = c(90, 85)
)
```

Now you want to include this data in your `reprex`.

🔹 Step 2: Run `dput(df)` in the console

```r
dput(df)
```

You'll see something like this printed:

```r
structure(list(name = c("Alice", "Bob"), score = c(90, 85)), 
  class = c("tbl_df", "tbl", "data.frame"), row.names = c(NA, -2L))
```

That’s ugly to read, but **exactly what R needs to rebuild `df` from scratch**.

🔹 Step 3: Paste into your reprex

In your reprex, do this:

```r
df <- structure(list(name = c("Alice", "Bob"), score = c(90, 85)), 
  class = c("tbl_df", "tbl", "data.frame"), row.names = c(NA, -2L))

df
#> # A tibble: 2 × 2
#>   name  score
#>   <chr> <dbl>
#> 1 Alice    90
#> 2 Bob      85
```

📦 Real-world use case

Let’s say you ran into an error like this:

```r
df %>% 
  filter(score > 90)
```

But you’re not sure why it’s not working. Instead of saying:

> “Here's my data — it's a dataframe with 20 columns — trust me.”

You give people this:

```r
df <- structure(...)  # full dput() output here
df %>% 
  filter(score > 90)
```

Now **any helper can just copy, paste, and run** — no external files needed.

---

    
3. Spend a little bit of time ensuring that your **code** is easy for others to read:

Finish by checking that you have actually made a reproducible example by **starting a fresh R session and copying and pasting your script.**
## 8.3 Investing in yourself

You should also spend some time preparing yourself to solve problems before they occur. Investing a little time in learning R each day will pay off handsomely in the long run. One way is to follow what the tidyverse team is doing on the [tidyverse blog](https://www.tidyverse.org/blog/). To keep up with the R community more broadly, we recommend reading [R Weekly](https://rweekly.org/): it’s a community effort to aggregate the most interesting news in the R community each week.

Indeed great resources