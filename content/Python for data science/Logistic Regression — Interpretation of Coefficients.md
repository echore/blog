---
share: true
---
2026-03-24  17:03
Tags:

---

# 1. Start from the core equation
$$
[  
\log\left(\frac{P}{1-P}\right)  
= \beta_0 + \beta_1 x_1 + \cdots + \beta_p x_p  
]
$$
Focus on one variable (x_j):
$$
[  
\log(\text{odds}) = \cdots + \beta_j x_j  
]
$$
---

# 2. What does (\beta_j) mean?

Think: increase (x_j) by 1

What happens?
$$
[  
\log(\text{odds}_{new}) - \log(\text{odds}_{old}) = \beta_j  
]
$$
So:

> A 1-unit increase in (x_j) changes **log-odds** by (\beta_j)

But log-odds is not intuitive.

So we exponentiate.

---

# 3. Convert to something interpretable
$$
[  
e^{\beta_j} = \text{odds ratio}  
]
$$
This is the key.

---

# 4. Final interpretation (memorize this)

> A 1-unit increase in (x_j) multiplies the **odds** by (e^{\beta_j})

---

# 5. Concrete example

Suppose:
$$
[  
\beta_{age} = -0.7  
]
$$
Then:
$$
[  
e^{-0.7} \approx 0.5  
]
$$
Interpretation:

> Each 1-year increase in age → odds are multiplied by 0.5  
> → odds are cut in half

---

Another example:
$$
[  
\beta_{score} = 0.7  
]
$$
$$
[  
e^{0.7} \approx 2  
]
$$
Interpretation:

> Each +1 in score → odds double

---

# 6. Important: this is NOT probability

This is where most people get confused.

You are NOT saying:

> probability increases by 0.2

You are saying:

> odds are multiplied by 2

---

# 7. Why odds instead of probability?

Because the relationship is nonlinear.

Example:

If baseline probability = 0.1  
odds = 0.11

Multiply odds by 2 → 0.22  
new probability ≈ 0.18

---

If baseline probability = 0.8  
odds = 4

Multiply odds by 2 → 8  
new probability ≈ 0.89

---

Same coefficient, very different probability change.

That’s why we use odds.

---

# 8. Direction vs magnitude

### Sign of coefficient

- (\beta > 0): increases probability
    
- (\beta < 0): decreases probability
    

---

### Magnitude

- larger (|\beta|) → stronger effect
    
- but better to compare using (e^{\beta})
    

---

# 9. Special case: binary variable

If:
$$
[  
x_j = 0 \text{ or } 1  
]
$$
Then:
$$
[  
e^{\beta_j}  
]
$$
means:

> odds for group 1 vs group 0

---

Example:

- gender (female = 1, male = 0)
    
- (e^{\beta} = 1.5)
    

Interpretation:

> females have 1.5× the odds compared to males

---

# 10. Intercept (\beta_0)
$$
[  
\beta_0 = \log(\text{odds when all } x=0)  
]
$$
Often not meaningful unless variables are centered.


---

# 12. Common mistakes

### Mistake 1

“β = 0.7 means probability increases by 0.7”

Wrong.

---

### Mistake 2

Comparing coefficients directly across scaled vs unscaled data

---

### Mistake 3

Ignoring that effect depends on baseline probability

---

# 13. Mental model

Think of logistic regression as:

- linear model → log-odds
    
- exponent → multiplicative effect on odds
    

---

# 14. One-line summary
$$
[  
\beta_j \Rightarrow \text{log-odds change}  
\quad\rightarrow\quad  
e^{\beta_j} \Rightarrow \text{odds multiplier}  
]
$$
---




---

# Example: Interpreting Logistic Regression Coefficients

## Model
$$
[  
\log\left(\frac{P}{1-P}\right) = -2 + 0.7 \cdot \text{tachycardia}  
]
$$
Where:

- `tachycardia = 1` → patient has tachycardia
    
- `tachycardia = 0` → no tachycardia
    

---

# Step 1: Baseline (no tachycardia)
$$
[  
\text{tachycardia} = 0  
]
$$
$$
[  
\log(\text{odds}) = -2  
]
$$
Convert to odds:
$$
[  
\text{odds} = e^{-2} \approx 0.135  
]
$$
Convert to probability:
$$
[  
P = \frac{0.135}{1 + 0.135} \approx 0.12  
]
$$
### Interpretation

> Without tachycardia, the probability of hospitalization is about **12%**

---

# Step 2: With tachycardia
$$
[  
\text{tachycardia} = 1  
]
$$
$$
[  
\log(\text{odds}) = -2 + 0.7 = -1.3  
]
$$
$$
[  
\text{odds} = e^{-1.3} \approx 0.27  
]
$$
$$
[  
P = \frac{0.27}{1 + 0.27} \approx 0.21  
]
$$
### Interpretation

> With tachycardia, the probability of hospitalization is about **21%**

---

# Step 3: What does the coefficient mean?

We focus on:
$$
[  
\beta = 0.7  
]
$$
Exponentiate:
$$
[  
e^{0.7} \approx 2  
]
$$
---

# Key Interpretation

> Having tachycardia **doubles the odds** of hospitalization

---

# Step 4: Verify numerically

- Original odds = 0.135
    
- New odds = 0.27
    
$$
[  
0.27 = 2 \times 0.135  
]
$$
So the interpretation is exact.

---

# Step 5: Important insight

### The coefficient affects:

> Odds (multiplicative change)

---

### Not:

> Probability (additive change)

---

# Step 6: Why probability change is not fixed

From the example:

- 12% → 21% (increase of 9%)
    

But if baseline were different:

### Suppose baseline = 50%

- odds = 1
    
- multiply by 2 → odds = 2
    
$$
[  
P = \frac{2}{1+2} = 0.67  
]
$$
Now:

- 50% → 67% (increase of 17%)
    

---

# Key Insight

Same coefficient:

- always multiplies odds by 2
    
- but probability change depends on baseline
    

---

# Step 7: Proper professional wording

You can write:

> The presence of tachycardia is associated with a 2-fold increase in the odds of hospitalization.

---
