---
share: true
---
2026-03-25  12:04
Tags:


---

# 1. What are we trying to estimate?

We have:
$$
[  
P(y=1 \mid X) = \sigma(\beta^T X)  
]
$$
We **don’t know** the parameters:
$$
[  
\beta = (\beta_0, \beta_1, ..., \beta_p)  
]
$$
Goal:

> Find the best (\beta) so that the model matches the data.

---

# 2. What does “best” mean?

This is the key question.

There are many possible (\beta).

We need a rule to choose the best one.

👉 Logistic regression uses:

> **Maximum Likelihood Estimation (MLE)**

---

# 3. Core idea of MLE (intuitive)

We choose parameters that make the **observed data most likely**.

---

## Think like this:

You observe data:

```text
X → y
```

Example:

|X|y|
|---|---|
|patient A|1|
|patient B|0|
|patient C|1|

Your model gives probabilities:

- A → 0.9
    
- B → 0.2
    
- C → 0.8
    

That’s good.

---

Now imagine a bad model:

- A → 0.1
    
- B → 0.9
    
- C → 0.2
    

That’s terrible.

---

So we want:

> a model that assigns **high probability to correct outcomes**

---

# 4. Likelihood for one data point

For one observation:

- if (y=1): probability = (p)
    
- if (y=0): probability = (1-p)
    

We can combine both cases into one formula:
$$
[  
P(y \mid x) = p^y (1-p)^{1-y}  
]

-$$--

## Why this works

- if (y=1):  
- $$
    [  
    p^1 (1-p)^0 = p  
    ]
    $$
- if (y=0):  
- $$
    [  
    p^0 (1-p)^1 = 1-p  
    ]
    $$

---

# 5. Likelihood for entire dataset

Assume independence:
$$
[  
L(\beta) = \prod_{i=1}^{n} p_i^{y_i}(1-p_i)^{1-y_i}  
]
$$
This is the **likelihood function**.

---

# 6. What does MLE do?

We choose (\beta) that:
$$
[  
\text{maximize } L(\beta)  
]
$$
Meaning:

> make the observed data as probable as possible

---

# 7. Why we use log-likelihood

The product is messy.

So we take log:
$$
[  
\ell(\beta) = \sum_{i=1}^{n}  
\left[  
y_i \log(p_i) + (1-y_i)\log(1-p_i)  
\right]  
]
$$
This is much easier to work with.

---

# 8. Loss function (important connection)

In ML, we minimize loss instead of maximizing likelihood.

So we define:
$$
[  
\text{Loss} = -\ell(\beta)  
]
$$
$$
[  
= -\sum \left[  
y \log(p) + (1-y)\log(1-p)  
\right]  
]
$$
This is called:

> **Log Loss / Cross-Entropy Loss**

---

# 9. Intuition of log loss

Let’s test it.

---

## Case 1: correct and confident

- true (y=1)
    
- predicted (p=0.9)
    
$$
[  
\log(0.9) \approx -0.1  
]
$$
Small loss → good

---

## Case 2: wrong and confident

- true (y=1)
    
- predicted (p=0.1)
    
$$
[  
\log(0.1) \approx -2.3  
]
$$
Huge loss → heavily punished

---

# 10. Why this is powerful

This loss:

- rewards correct predictions
    
- punishes confident wrong predictions strongly
    
- is smooth and differentiable
    

---

# 11. How we actually find β

We cannot solve it analytically.

So we use optimization:

- Gradient Descent
    
- or solvers like LBFGS (used in sklearn)
    

---

# 12. What is happening during training?

Iteratively:

1. guess β
    
2. compute probabilities
    
3. compute loss
    
4. update β
    
5. repeat until convergence
    

---

# 13. Key insight (this is the real takeaway)

Logistic Regression is:

> a probabilistic model  
> trained by maximizing likelihood  
> equivalent to minimizing log-loss

---

# 14. Why not use MSE?

If we used:
$$
[  
(y - p)^2  
]
$$
Problems:

- not probabilistically correct
    
- non-convex (harder optimization)
    
- weaker penalties for wrong confident predictions
    

---

# 15. Connection to your project

In EMS prediction:

MLE ensures:

- if patient actually deteriorates
    
- model tries to assign high probability
    

So:

- better calibration
    
- better ranking
    
- meaningful probabilities
    

---

# 16. One-line summary

MLE chooses parameters that make the observed outcomes most probable under the model.

---
