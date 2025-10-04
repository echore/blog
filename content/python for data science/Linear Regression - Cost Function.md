---
share: true
---
2025-10-04  11:20
Tags:
# Linear Regression and the Cost Function

## 1. Prediction Function (Hypothesis)

We assume $y$ can be predicted as a **linear combination of inputs**:

$$
\hat{y} = \sum_{i=0}^n \beta_i x_i
$$

- $\hat{y}$ = predicted value  
- $x_i$ = input features (with $x_0 = 1$ for the intercept term)  
- $\beta_i$ = parameters (weights) we want to learn  

---

## 2. Error (Residual)

For each data point $j$, the error is:

$$
\text{error}^j = y^j - \hat{y}^j
$$

- $y^j$ = actual value  
- $\hat{y}^j$ = predicted value  

---

## 3. Cost Function (Squared Error)

We want to measure how "bad" our predictions are.  
So we square the errors and average them:

**Mean Squared Error (MSE):**

$$
\frac{1}{m} \sum_{j=1}^m \left( y^j - \hat{y}^j \right)^2
$$

where $m$ = number of rows (data points).  

To make derivative math cleaner, we add $\tfrac{1}{2}$:

**Cost function:**

$$
J(\beta) = \frac{1}{2m} \sum_{j=1}^m \left( y^j - \hat{y}^j \right)^2
$$

---

## 4. Why the 1/2m Factor?

- Dividing by $m$ gives us the **average** error.  
- The $\tfrac{1}{2}$ is just for **convenience**:  
  when we differentiate, the "2" from squaring cancels out.

---

## 5. Minimization via Calculus

We want to minimize $J(\beta)$.  
From calculus: **take derivative, set = 0**.

Gradient for parameter $\beta_k$:

$$
\frac{\partial J}{\partial \beta_k} 
= \frac{1}{m} \sum_{j=1}^m \left( y^j - \sum_{i=0}^n \beta_i x_i^j \right)(-x_k^j)
$$


---

## Intuition

1. Prediction: draw a line $\hat{y} = \alpha + \beta x$.  
2. Error: check how far actual points are from the line.  
3. Cost function: square errors, average them → get a "badness score".  
4. Gradient descent: follow the slope downhill to find the best line.
