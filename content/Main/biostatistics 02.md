---
share: true
---
2025-09-21  22:43
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










# Newton–Raphson Method

## 1. What is it?
The Newton–Raphson method is an **iterative algorithm** for finding solutions to equations of the form:
$$
f(x) = 0
$$

In optimization, we often want to find the **maximum or minimum** of a function.  
Since extrema occur when the derivative is zero:
$$
f'(x) = 0
$$
the problem becomes one of **root-finding** for the derivative function.

---

## 2. The update formula
The Newton–Raphson update rule is:
$$
x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}
$$

- \(x_k\): current guess  
- \(f(x_k)\): function value at the guess  
- \(f'(x_k)\): slope (derivative) at the guess  

---

## 3. Intuition
- At each step, approximate the curve \(f(x)\) by its **tangent line** at the current point.  
- Find where this tangent line crosses the x-axis.  
- Use that crossing as the new guess \(x_{k+1}\).  
- Repeat until convergence.

This works because tangents usually point directly toward the root.

---

## 5. Application in statistics
- In Maximum Likelihood Estimation (MLE), we want to maximize the log-likelihood \(\ell(\theta)\).  
- First derivative = score function:
$$
U(\theta) = \frac{\partial \ell(\theta)}{\partial \theta}
$$
- MLE solves \(U(\theta) = 0\).  
- Newton–Raphson can be used to solve this equation.

General update:
$$
\theta_{k+1} = \theta_k - \frac{U(\theta_k)}{U'(\theta_k)}
$$

Here \(U'(\theta)\) is the second derivative (the Hessian in multivariate cases).

---

## 6. Key features
- **Fast convergence**: if the starting point is close to the true root.  
- **Requires derivatives**: both first and sometimes second derivatives.  
- **Used widely**: in optimization, MLE, logistic regression, and nonlinear models.

---

## ✅ Summary
- Newton–Raphson = root-finding algorithm.  
- Formula: \(x_{k+1} = x_k - f(x_k)/f'(x_k)\).  
- In optimization: solve \(f'(x) = 0\).  
- In statistics: used to find MLEs by solving the score equation.  
- Powerful, but needs a good starting guess and derivatives.





# Why do we solve f(x) = 0 in optimization?

## 1. Optimization goal
In statistics, we often want to **maximize or minimize a function**.  
Example: Maximum Likelihood Estimation (MLE) = find the parameter that maximizes the log-likelihood.

---

## 2. First-order condition
At a maximum or minimum, the **slope of the function is zero**:
$$
f'(x) = 0
$$

This is called the *first-order necessary condition*.

---

## 3. Why does this become a root-finding problem?
- Saying *“find the maximum”* is equivalent to saying *“solve the equation f'(x) = 0.”*  
- In other words, we are looking for the **root** of the derivative function.

Formally:
$$
g(x) = f'(x), \quad g(x) = 0
$$

So optimization = root-finding applied to the derivative.

---

## 4. Example
Suppose:
$$
f(x) = -x^2 + 4x
$$

1. Derivative:
$$
f'(x) = -2x + 4
$$

2. Solve:
$$
-2x + 4 = 0 \quad \Rightarrow \quad x = 2
$$

3. Therefore, the maximum occurs at \(x=2\).

---

## 5. Why Newton–Raphson?
- If the derivative equation \(f'(x) = 0\) is simple, we can solve it directly.  
- But in most real problems (e.g., in MLE), \(f'(x)\) is complex and has no closed-form solution.  
- Newton–Raphson gives us an **iterative method** to approximate the solution step by step.

---

## ✅ Key takeaway
- Optimization requires solving \(f'(x) = 0\).  
- That is a **root-finding problem**.  
- Newton–Raphson is a general algorithm for root-finding, so it is used to solve for maxima/minima in statistics.





# Newton–Raphson Method: Why This Formula?


---

## Why does the Newton–Raphson formula look like that?

The update rule is:
$$
x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}
$$

This comes from the **tangent line approximation**.

### Step A: Approximate by tangent line
Near $x_k$, approximate $f(x)$ by its tangent:
$$
f(x) \approx f(x_k) + f'(x_k)(x - x_k)
$$

### Step B: Solve for the root of the line
Set this equal to zero:
$$
0 = f(x_k) + f'(x_k)(x - x_k)
$$

Solve for $x$:
$$
x = x_k - \frac{f(x_k)}{f'(x_k)}
$$

👉 That’s the Newton–Raphson formula.

---

## 3. Intuition: Why does this work?

- Each step: *“Pretend the function is a straight line here. Where does that line cross the x-axis?”*
- Move your guess to that crossing.
- Repeat → gets closer to the true root (if the function is smooth).

---

## 4. Connecting back to statistics

- MLE requires solving:
$$
U(\theta) = \frac{\partial \ell(\theta)}{\partial \theta} = 0
$$
- Newton–Raphson provides a way to solve this iteratively when no closed-form solution exists.
- Because the log-likelihood is often concave, the method converges quickly to the maximum.

---



# Newton–Raphson Method Example

---

## Problem
Find $\sqrt{2}$ by solving:
$$
f(x) = x^2 - 2 = 0
$$

---

## Step 1: Function and derivative
- Function: $f(x) = x^2 - 2$
- Derivative: $f'(x) = 2x$

---

## Step 2: Newton–Raphson update rule
$$
x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}
= x_k - \frac{x_k^2 - 2}{2x_k}
$$

---

## Step 3: Iterations

- Start with $x_0 = 1$.

1. First iteration:
$$
x_1 = 1 - \frac{1^2 - 2}{2 \cdot 1} = 1 - \frac{-1}{2} = 1.5
$$

2. Second iteration:
$$
x_2 = 1.5 - \frac{1.5^2 - 2}{2 \cdot 1.5}
= 1.5 - \frac{0.25}{3} \approx 1.4167
$$

3. Third iteration:
$$
x_3 = 1.4167 - \frac{1.4167^2 - 2}{2 \cdot 1.4167}
\approx 1.4142
$$

---

## Step 4: Result
After only 3 iterations, we get:
$$
x_3 \approx 1.4142
$$

which is accurate to 4 decimal places (the true value $\sqrt{2} \approx 1.4142$).

---

## ✅ Key Lesson
- Newton–Raphson converges **very quickly** if the function is smooth.
- Each step uses the tangent line at the current guess to jump closer to the root.
- In statistics, the exact same method is used to solve the score equation for MLEs.

# Newton–Raphson: Starting Point and Convergence

---

## 1. Why start with $x_0 = 1$?

- Newton–Raphson requires an **initial guess**.
- It does not have to be perfect, but should be close to the root.
- For the equation $x^2 - 2 = 0$:
  - $1^2 = 1 < 2$
  - $2^2 = 4 > 2$
- So the root $\sqrt{2}$ must lie between 1 and 2.
- Choosing $x_0 = 1$ (or $x_0 = 2$) is a reasonable starting point.

👉 In practice: the starting guess often comes from prior knowledge or rough estimates of the parameter.

---

## 2. Why does it converge so quickly?

- Newton–Raphson uses the **tangent line**, which is a very accurate local approximation if the function is smooth.
- Each iteration roughly **doubles the number of correct digits** (this is called *quadratic convergence*).

Example for $\sqrt{2}$:
- After 1 step: $x_1 = 1.5$ (close).
- After 2 steps: $x_2 = 1.4167$ (closer).
- After 3 steps: $x_3 = 1.4142$ (correct to 4 decimals).

---

## 3. Why stop after 3 iterations?

In practice we do not know the true root in advance. We stop when:

- The updates are very small:
$$
|x_{k+1} - x_k| < \text{tolerance}
$$

- Or when the function value is close to zero:
$$
|f(x_k)| < \text{tolerance}
$$

Example:
$$
f(1.4142) = (1.4142)^2 - 2 \approx 0.000006
$$
This is close enough to zero, so the algorithm has **converged**.

---

## ✅ Key Takeaways

- Start with a reasonable guess near the root.
- Newton–Raphson converges very fast if the function is smooth and well-behaved.
- Stopping rules are based on how small the update or the function value becomes.
