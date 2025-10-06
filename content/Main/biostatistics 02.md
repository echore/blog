---
share: true
---
2025-10-06  13:32
Tags:[[Bordeaux|Bordeaux]]

# Two-sample t-test Example

# What is a t-test?

A **t-test** is a statistical test that compares **means** (averages).  
It asks:

> “Are the observed differences in means big enough that they’re unlikely to be due to random chance?”

**Question:** Do mothers of low-birth-weight babies have a different average weight compared to mothers of normal-birth-weight babies?

---

## Step 1: Hypotheses
- Null hypothesis:
$$
H_0: \mu_{\text{low}} = \mu_{\text{normal}}
$$

- Alternative hypothesis:
$$
H_a: \mu_{\text{low}} \neq \mu_{\text{normal}}
$$

---

## Step 2: Sample data (illustration)

- Group 1 (low BW mothers):  
  $n_1 = 10, \quad \bar{x}_1 = 115, \quad s_1 = 10$

- Group 2 (normal BW mothers):  
  $n_2 = 12, \quad \bar{x}_2 = 130, \quad s_2 = 12$

---

## Step 3: Formula for two-sample t-test (equal variances)

1. **Pooled variance:**
$$
s_p^2 = \frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2}
$$

2. **Standard error (SE):**
$$
SE = s_p \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}
$$

3. **t-statistic:**
$$
t = \frac{\bar{x}_1 - \bar{x}_2}{SE}
$$

---

## Step 4: Plug in numbers

1. Pooled variance:
$$
s_p^2 = \frac{(10-1)(10^2) + (12-1)(12^2)}{10+12-2}
= \frac{900 + 1584}{20}
= 124.2
$$

So pooled SD:
$$
s_p = \sqrt{124.2} \approx 11.15
$$

2. Standard error:
$$
SE = 11.15 \cdot \sqrt{\frac{1}{10} + \frac{1}{12}}
= 11.15 \cdot \sqrt{0.1833}
= 11.15 \cdot 0.428 \approx 4.77
$$

3. t-statistic:
$$
t = \frac{115 - 130}{4.77}
= \frac{-15}{4.77}
\approx -3.15
$$

---

## Step 5: Decision

- Degrees of freedom:
$$
df = n_1 + n_2 - 2 = 20
$$

- Critical value (two-sided, $\alpha=0.05$): $\pm 2.086$

- Our test statistic: $t = -3.15$

Since $|t| > 2.086$, we **reject $H_0$**.

---

## ✅ Conclusion
There is a **significant difference** in maternal weights between mothers of low vs. normal birth weight babies (p < 0.01).


# Chi-square Test of Independence Example
# 1. What is a chi-square test?

A **chi-square test** is used for **categorical variables** (yes/no, male/female, race groups, etc.).

It answers questions like:

> “Are these two categorical variables related, or are they independent?”  
> “Do proportions differ across groups?”

---

## Step 1: Hypotheses
- Null hypothesis:
$$
H_0: \text{Proportion of low birth weight infants is the same across races}
$$

- Alternative hypothesis:
$$
H_a: \text{Proportion of low birth weight infants differs by race}
$$

---

## Step 2: Sample data (illustration)

| Race   | Low BW (1) | Normal BW (0) | Total |
|--------|------------|---------------|-------|
| White  | 20         | 180           | 200   |
| Black  | 15         | 85            | 100   |
| Other  | 10         | 90            | 100   |
| **Total** | 45     | 355           | 400   |

---

## Step 3: Expected counts

Formula:
$$
E_{ij} = \frac{\text{Row total} \times \text{Column total}}{\text{Grand total}}
$$

Example for White–Low BW:
$$
E = \frac{200 \times 45}{400} = 22.5
$$

Do this for each cell.

---

## Step 4: Compute chi-square statistic

Formula:
$$
\chi^2 = \sum \frac{(O - E)^2}{E}
$$

Let’s calculate a few cells:

- White–Low BW:
$$
\frac{(20 - 22.5)^2}{22.5} = \frac{6.25}{22.5} \approx 0.278
$$

- Black–Low BW:
$$
\frac{(15 - 11.25)^2}{11.25} = \frac{14.06}{11.25} \approx 1.25
$$

- Other–Low BW:
$$
\frac{(10 - 11.25)^2}{11.25} = \frac{1.56}{11.25} \approx 0.139
$$

… and similarly for the “Normal BW” cells.

Add them all up:
$$
\chi^2 \approx 2.39
$$

---

## Step 5: Decision

- Degrees of freedom:
$$
df = (\text{rows}-1)(\text{cols}-1) = (3-1)(2-1) = 2
$$

- Critical value (α = 0.05, df = 2): 5.99

- Our test statistic: $\chi^2 = 2.39$

Since $2.39 < 5.99$, we **fail to reject $H_0$**.

---

## ✅ Conclusion
There is **no significant evidence** that the proportion of low birth weight infants differs across racial groups (p > 0.05).



---
# Conclusion

# 🧩 Step 1: What are we comparing?

The table is all about **bivariate comparisons** — comparing an outcome (dependent variable) across one or more groups (independent variable).

Two key questions:

1. Is the **outcome variable** continuous (a number like weight, height, blood pressure) or categorical (like yes/no, race, low vs normal)?
    
2. How many groups are we comparing? (1, 2, or more?)
    

---

# 🧩 Step 2: Continuous outcomes

If your dependent variable is **continuous**:

### a) One group vs. a fixed value

- Example: Is the average maternal weight = 120 pounds?
    
- **Test:** One-sample t-test (parametric) or Wilcoxon signed-rank test (nonparametric).
    
- **Why?** Because you’re comparing the sample mean/median to a known constant.
    

---

### b) Two independent groups

- Example: Is mean maternal weight different for low vs. normal birth weight infants?
    
- **Test:** Two-sample t-test (parametric) or Mann–Whitney U (nonparametric).
    
- **Why?** Because you want to compare averages of **two groups**.
    

---

### c) More than two groups

- Example: Is mean infant birth weight different across 3 race categories?
    
- **Test:** ANOVA (parametric) or Kruskal–Wallis test (nonparametric).
    
- **Why?** ANOVA extends the t-test idea to more than 2 groups.
    

---

### d) Two matched/paired groups

- Example: Compare a mother’s blood pressure before pregnancy vs. during pregnancy (same person, measured twice).
    
- **Test:** Paired t-test (parametric) or Wilcoxon signed-rank test (nonparametric).
    
- **Why?** Because the data points are _linked_ (paired).
    

---

# 🧩 Step 3: Categorical outcomes

If your dependent variable is **categorical** (yes/no, or categories like race):

### a) Two independent groups

- Example: Compare proportion of low birth weight in smokers vs. non-smokers.
    
- **Test:** z-test for proportions (parametric) or Chi-square test (nonparametric). If sample is small, Fisher’s exact test.
    
- **Why?** Because you’re comparing proportions between 2 groups.
    

---

### b) More than two groups

- Example: Does the proportion of low birth weight differ across 3 races?
    
- **Test:** Chi-square test of independence.
    
- **Why?** Because chi-square is the standard tool for comparing categorical distributions across groups.
    

---

### c) Paired/matched binary data

- Example: Did the same baby get classified as “low birth weight” by **two doctors**? (paired yes/no outcomes).
    
- **Test:** McNemar’s test.
    
- **Why?** Because it’s for paired categorical data (think 2x2 table with matched pairs).
    

---

# 🧩 Step 4: Continuous vs Continuous

- Example: Is maternal weight correlated with infant birth weight?
    
- **Test:** Pearson’s correlation (parametric) or Spearman’s correlation (nonparametric).
    
- **Why?** Because both are continuous, and you’re looking for association.
    

---

# 🧩 Step 5: Parametric vs. Nonparametric

- **Parametric tests** (t-test, ANOVA, z-test, Pearson) assume the data follow certain distributions (usually normal).
    
- **Nonparametric tests** (Wilcoxon, Mann–Whitney, Kruskal–Wallis, Spearman, Fisher’s exact) don’t rely on those assumptions.
    
- Rule of thumb: if sample size is small or data are skewed/outliers → go nonparametric.
    

---

# ✅ In plain words:

- If your outcome is **continuous** → you’re comparing means → use t-test (2 groups), ANOVA (≥3 groups), or paired t-test.
    
- If your outcome is **categorical** → you’re comparing proportions → use chi-square, z-test, or Fisher’s exact.
    
- If both are continuous → use correlation (Pearson or Spearman).
    

---



# Two-sample z-test (with known variances)

**Question:** Do two independent populations have the same mean, assuming their variances are known?

---

## Step 1: Hypotheses

- Null hypothesis:
$$
H_0: \mu_1 = \mu_2 \quad \text{or} \quad \mu_1 - \mu_2 = 0
$$

- Alternative hypothesis (depends on question):
$$
H_a: \mu_1 \neq \mu_2 \quad \text{(two-sided)}
$$
or
$$
H_a: \mu_1 > \mu_2 \quad \text{(one-sided)}
$$

---

## Step 2: Sampling distribution of the difference

The sample means are:
$$
\bar{X}_1, \quad \bar{X}_2
$$

The difference has expectation:
$$
E[\bar{X}_1 - \bar{X}_2] = \mu_1 - \mu_2
$$

And variance:
$$
\text{Var}(\bar{X}_1 - \bar{X}_2) = \frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}
$$

So the **standard error (SE)** is:
$$
SE = \sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}
$$

---

## Step 3: Test statistic

Under $H_0: \mu_1 - \mu_2 = 0$:
$$
Z = \frac{(\bar{X}_1 - \bar{X}_2) - 0}{SE}
= \frac{\bar{X}_1 - \bar{X}_2}{\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}}
$$

---

## Step 4: Decision rule

- Choose significance level $\alpha$ (e.g., 0.05).
- Two-sided test: reject $H_0$ if $|Z| > z_{\alpha/2}$.
- One-sided test: reject $H_0$ if $Z > z_\alpha$ or $Z < -z_\alpha$.
- Or compute the p-value and compare with $\alpha$.

---

## Step 5: Numerical Example

Suppose:
- Population 1: $\sigma_1^2 = 25$, $n_1 = 50$, $\bar{X}_1 = 100$
- Population 2: $\sigma_2^2 = 36$, $n_2 = 60$, $\bar{X}_2 = 95$

**A. Compute SE**
$$
SE = \sqrt{\frac{25}{50} + \frac{36}{60}} = \sqrt{0.5 + 0.6} = \sqrt{1.1} \approx 1.048
$$

**B. Test statistic**
$$
Z = \frac{100 - 95}{1.048} \approx \frac{5}{1.048} \approx 4.77
$$

**C. Decision**
- Degrees of freedom: not needed (Z test uses normal distribution).
- Critical value for two-sided $\alpha = 0.05$: $z_{0.025} = 1.96$.
- Our $Z = 4.77 > 1.96$.

✅ Reject $H_0$.

---

## ✅ Conclusion

There is a **significant difference** between the two population means (p < 0.01).



