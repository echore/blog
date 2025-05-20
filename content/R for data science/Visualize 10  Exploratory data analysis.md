---
share: true
date: 2025-05-20
---
## 10.2 Questions
There is no rule about which questions you should ask to guide your research. However, two types of questions will always be useful for making discoveries within your data. You can loosely word these questions as:

1. What type of variation occurs within my variables?
    
2. What type of covariation occurs between my variables?

## 10.3 Variation
### 10.3.1 Typical values

In both bar charts and histograms, tall bars show the common values of a variable, and shorter bars show less-common values. Places that do not have bars reveal values that were not seen in your data. To turn this information into useful questions, look for anything unexpected:

- Which values are the most common? Why?
    
- Which values are rare? Why? Does that match your expectations?
    
- Can you see any unusual patterns? What might explain them?

```r
ggplot(diamonds,aes(x = carat)) +
  geom_histogram(binwidth = 0.6)
```

```r
smaller <- diamonds %>% 
  filter(carat < 3)

ggplot(smaller, aes(x = carat)) +
  geom_histogram(binwidth = 0.05)
```

![[Pasted image 20250520155832.png|Pasted image 20250520155832.png]]

This histogram suggests several interesting questions:

- Why are there more diamonds at whole carats and common fractions of carats?
    
- Why are there more diamonds slightly to the right of each peak than there are slightly to the left of each peak?
    

Visualizations can also reveal clusters, which suggest that subgroups exist in your data. To understand the subgroups, ask:

- How are the observations within each subgroup similar to each other?
    
- How are the observations in separate clusters different from each other?
    
- How can you explain or describe the clusters?
    
- Why might the appearance of clusters be misleading?

### 10.3.2 Unusual values

```r
ggplot(diamonds, aes(x = y)) + 
  geom_histogram(binwidth = 0.5)
```
To make it easy to see the unusual values, we need to zoom to small values of the y-axis with `coord_cartesian()`:

```r
ggplot(diamonds,aes(x = y)) +
  geom_histogram(binwidth = 0.5) +
  coord_cartesian(ylim = c(0,50))
```
![[Pasted image 20250520160648.png|Pasted image 20250520160648.png]]

This allows us to see that there are three unusual values: 0, ~30, and ~60. We pluck them out with dplyr:
```r
unusual <- diamonds %>% 
  filter(y < 3 | y > 20) %>% 
  select(price, x, y, z) %>% 
  arrange(y)
unusual
A tibble: 9 × 4
  price     x     y     z
  <int> <dbl> <dbl> <dbl>
1  5139  0      0    0   
2  6381  0      0    0   
3 12800  0      0    0   
4 15686  0      0    0   
5 18034  0      0    0   
6  2130  0      0    0   
7  2130  0      0    0   
8  2075  5.15  31.8  5.12
9 12210  8.09  58.9  8.06
```
The `y` variable measures one of the three dimensions of these diamonds, in mm. We know that diamonds can’t have a width of 0mm, so these values must be incorrect. By doing EDA, we have discovered missing data that was coded as 0, which we never would have found by simply searching for `NA`s. Going forward we might choose to re-code these values as `NA`s in order to prevent misleading calculations. 

We might also suspect that measurements of 32mm and 59mm are implausible: those diamonds are over an inch long, but don’t cost hundreds of thousands of dollars!

### 10.3.3 Exercises
1. Explore the distribution of `price`. Do you discover anything unusual or surprising? (Hint: Carefully think about the `binwidth` and make sure you try a wide range of values.)
```r
ggplot(diamonds,aes(x = price)) +
  geom_histogram()
```
![[Pasted image 20250520162112.png|Pasted image 20250520162112.png]]
It’s heavily **right-skewed**: most diamonds are under $5,000. SO:

```r
ggplot(diamonds,aes(x = price)) +
  geom_histogram(binwidth = 100) + 
  coord_cartesian(xlim = c(0,5000))
```
![[Pasted image 20250520162144.png|Pasted image 20250520162144.png]]
2. How many diamonds are 0.99 carat? How many are 1 carat? What do you think is the cause of the difference?

```r
diamonds %>% 
  filter(carat == 0.99 | carat == 1) %>% 
  count(carat)
```

See it visually
```r
ggplot(diamonds, aes(x = carat)) +
  geom_histogram(binwidth = 0.01) +
  coord_cartesian(xlim = c(0.95,1.05))
```
![[Pasted image 20250520162533.png|Pasted image 20250520162533.png]]
## 10.4 Unusual values
