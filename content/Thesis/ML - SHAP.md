---
share: true
---
2026-03-09  16:27
Tags:[[Technical Literacy|Technical Literacy]]

---

# 1. The Core Idea Behind SHAP

SHAP comes from **Shapley values in cooperative game theory**.

Imagine a team wins **$100**.  
Several players contributed. The question is:

> How much credit should each player get?

The Shapley solution calculates **each player’s fair contribution**.

In ML:

```
players  → features
reward   → prediction
```

So SHAP distributes the prediction across features.

Example prediction:

```
Predicted risk = 0.42
Baseline risk = 0.08
```

SHAP decomposes the difference:

```
0.42 = 0.08
     + Age contribution
     + Shock index contribution
     + GCS contribution
     + Blood pressure contribution
```

Each feature receives a **numerical contribution value**.

---

# 2. Why SHAP Became Popular

Earlier interpretability tools had problems.

### Feature importance (old method)

Example output:

```
Age          0.25
Shock index  0.22
GCS          0.15
```

But this only tells you:

```
which variables matter
```

It does NOT tell you:

- whether the feature increases or decreases risk
    
- how much it changed an individual prediction
    

---

### SHAP solves this

SHAP shows:

```
importance
direction
magnitude
patient-level explanation
```

Example:

|Feature|SHAP|
|---|---|
|Age|+0.12|
|Shock index|+0.18|
|Normal BP|−0.04|

So we know **exactly how each variable moved the prediction**.

---

# 3. Local vs Global SHAP

Two important ways SHAP is used.

---

### Local explanation

Explains **one prediction**.

Example:

```
Prediction = 0.42
```

Drivers:

```
Shock index  +0.18
Age          +0.12
Low GCS      +0.08
```

Protective factors:

```
Normal BP    −0.04
```

This explains **why the model classified this patient as high risk**.

---

### Global explanation

We average SHAP values across the dataset.

Example:

|Feature|Mean SHAP|
|---|---|
|Shock index|highest|
|Age|high|
|GCS|medium|

This tells us **which predictors drive the model overall**.

---

# 4. SHAP Summary Plot (Most Famous Visualization)

This plot is extremely common in ML papers.

Each dot represents **one patient**.

Example idea:

```
feature: Shock index
```

Dots:

```
red = high shock index
blue = low shock index
```

Horizontal axis:

```
SHAP value
```

Meaning:

```
positive SHAP → increases predicted risk
negative SHAP → decreases predicted risk
```

This lets you see **how feature values influence predictions**.

---

# 5. SHAP Interaction Effects

SHAP can also detect **feature interactions**.

Example:

Shock index might have stronger effect when:

```
Age > 75
```

Meaning:

```
Age modifies the effect of shock index
```

Tree models capture these interactions automatically.

SHAP helps reveal them.

---

# 6. Why SHAP Works Well for Tree Models

Many models today use **tree ensembles**:

- Random Forest
    
- XGBoost
    
- LightGBM
    

The SHAP algorithm **TreeSHAP** can compute exact Shapley values efficiently for these models.

That’s why SHAP is widely used with boosting models.

---

# 7. Important Limitations

SHAP is powerful but not perfect.

### 1. Not causal

SHAP explains **model behavior**, not real-world causality.

Example:

```
Age has high SHAP value
```

This means the model **uses age strongly**.

It does NOT mean:

```
age causes adverse outcome
```

---

### 2. Correlated features

If features are correlated:

```
pulse
heart rate
shock index
```

SHAP may distribute importance across them in complex ways.

Interpretation becomes harder.

---

### 3. Computational cost

SHAP calculations can be expensive for large datasets.

TreeSHAP solves this for tree models.

---

# 8. When You Should Use SHAP

SHAP is most useful when:

- model is complex (Random Forest, XGBoost)
    
- interpretability is required
    
- stakeholders need explanation
    

This is especially common in:

```
healthcare
finance
risk prediction
```

---

# 9. Best SHAP Learning Resources

Here are the **best explanations online**.

---

### 1️⃣ Official SHAP documentation

Very clear explanations and examples.

[https://shap.readthedocs.io](https://shap.readthedocs.io/)

Start with:

```
SHAP values overview
```

---

### 2️⃣ The original SHAP paper

The foundational research paper:

Lundberg & Lee (2017)

[https://arxiv.org/abs/1705.07874](https://arxiv.org/abs/1705.07874)

Title:

```
A Unified Approach to Interpreting Model Predictions
```

---

### 3️⃣ Excellent visual tutorial

[https://christophm.github.io/interpretable-ml-book/shap.html](https://christophm.github.io/interpretable-ml-book/shap.html)

This website (Interpretable ML book) is one of the **best explainable ML resources**.

It explains:

- SHAP
    
- LIME
    
- feature importance
    
- PDP
    

---

### 4️⃣ StatQuest video

Josh Starmer explains SHAP very clearly:

[https://www.youtube.com/watch?v=9u9xZ7eH6mA](https://www.youtube.com/watch?v=9u9xZ7eH6mA)

His videos are great for intuition.

---

# 10. One Concept Worth Remembering

The key idea:

```
Prediction
=
baseline prediction
+ contributions from features
```

SHAP assigns those contributions **fairly using game theory**.

---

If you want, the **next concept that fits perfectly with SHAP** (and is also common in prediction papers) is:

**Partial Dependence Plots (PDP)**

They show:

```
how changing a variable changes predicted risk
```

across the population.
