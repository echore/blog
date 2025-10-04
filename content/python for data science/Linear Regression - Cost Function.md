---
share: true
---
2025-10-04  11:20
Tags:
# Cost Function (in Machine Learning / Regression)

## What is a Cost Function?

- A **cost function** (sometimes called a "loss function") tells us **how bad our model is**.  
- It measures the difference between the model’s predictions $\hat{y}$ and the actual values $y$.  
- The smaller the cost function, the better the model fits the data.  
- Training a model = **finding parameters (like $\alpha, \beta$) that minimize the cost function**.

---

## Linear Regression

We predict $y$ from $x$ with a line:

$$
\hat{y}_i = \alpha + \beta x_i
$$

The **residual** for each point is:

$$
\varepsilon_i = y_i - \hat{y}_i
$$

The cost function is the **sum of squared errors (SSE)**:

$$
J(\alpha, \beta) = \sum_{i=1}^n (y_i - \hat{y}_i)^2
$$

or equivalently:

$$
J(\alpha, \beta) = \sum_{i=1}^n (y_i - (\alpha + \beta x_i))^2
$$

---

