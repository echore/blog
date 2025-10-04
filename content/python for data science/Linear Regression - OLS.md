---
share: true
---
2025-10-04  11:06
Tags:

# OLS Regression

We want to fit a line:

$$
y_i \approx \alpha + \beta x_i
$$

by minimizing the **sum of squared residuals**:

$$
Q(\alpha,\beta) = \sum_{i=1}^n (y_i - \alpha - \beta x_i)^2
$$

---

## Step 1: Minimize w.r.t. α

Take derivative:

$$
\frac{\partial Q}{\partial \alpha} = -2\sum_{i=1}^n (y_i - \alpha - \beta x_i) = 0
$$

$$
\Rightarrow \hat{\alpha} = \bar{y} - \hat{\beta}\bar{x}
$$

---

## Step 2: Minimize w.r.t. β

Take derivative:

$$
\frac{\partial Q}{\partial \beta} = -2\sum_{i=1}^n x_i (y_i - \alpha - \beta x_i) = 0
$$

Substitute $\alpha = \bar{y} - \beta\bar{x}$:

$$
\sum (x_i - \bar{x})(y_i - \bar{y}) - \beta \sum (x_i - \bar{x})^2 = 0
$$

So the slope is:

$$
\hat{\beta} = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}
$$

---

## Step 3: Intuition

- **Numerator**:  
  $\sum (x_i - \bar{x})(y_i - \bar{y}) = n \cdot \text{Cov}(x,y)$  
  → measures how much $x$ and $y$ move together.

- **Denominator**:  
  $\sum (x_i - \bar{x})^2 = n \cdot \text{Var}(x)$  
  → measures how spread out $x$ is.

- Therefore:

$$
\hat{\beta} = \frac{\text{Cov}(x,y)}{\text{Var}(x)}
$$

