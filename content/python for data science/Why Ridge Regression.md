---
share: true
---
2026-03-11  14:10
Tags:

---

# 1. First: RSS Alone Can Encourage Overfitting

Ordinary linear regression minimizes only:
$$
RSS = \sum_{i=1}^{n}(y_i-\hat{y}_i)^2
$$
This objective says:

> “Find coefficients that make predictions as close as possible to the training data.”

But notice something important:

**RSS does not care how big the coefficients become.**

The model is allowed to do things like:

```
y = 120x1 − 98x2 + 350x3 − 500x4
```

If those numbers reduce RSS, the algorithm is happy.

But this creates a problem.

---

# 2. Why Large Coefficients Are Dangerous

Large coefficients mean the model becomes **extremely sensitive**.

Example:

```
y = 300 * x
```

If `x` changes slightly:

```
x = 2.00 → y = 600
x = 2.01 → y = 603
```

A tiny change in input → big change in prediction.

Now imagine many features:

```
y = 200x1 − 180x2 + 95x3 − 250x4 ...
```

The model becomes **unstable**.

This instability means:

```
small noise in training data
→ huge change in coefficients
→ bad predictions on new data
```

That is **overfitting**.

---

# 3. Overfitting Is Not Detected from RSS Alone

This is key:

You **cannot detect overfitting by looking only at training RSS**.

Training RSS will always go down as the model becomes more flexible.

Example:

|Model|Train Error|Test Error|
|---|---|---|
|simple|medium|medium|
|complex|very low|high|

The complex model looks better on training data but worse on new data.

So we detect overfitting by comparing:

```
training error vs test error
```

or via **cross-validation**.

---

# 4. Why Shrinking Coefficients Helps

Regularization changes the objective to:
$$
Loss = RSS + \alpha \sum_{j=1}^{p}\beta_j^2
$$
Now the model must balance two goals:

```
1️⃣ Fit the data well (low RSS)
2️⃣ Keep coefficients small
```

This forces the model to prefer **simpler relationships**.

Instead of:

```
y = 200x1 − 180x2 + 95x3
```

It might learn:

```
y = 2.3x1 − 1.8x2 + 0.7x3
```

The predictions become **more stable**.

---

# 5. Intuition: Smooth Models Generalize Better

Large coefficients create **wiggly models** that chase noise.

Small coefficients produce **smoother models**.

Imagine fitting points with a curve:

Overfit model:

```
~ ~ ~ ~ ~ ~ ~ ~
```

Simple model:

```
———
```

The smoother model usually predicts **new data** better.

---

# 6. Another Deep Reason: Multicollinearity

In real datasets, many variables are correlated.

Example in medicine:

```
blood pressure
heart rate
shock index
age
```

These variables interact.

Without regularization, regression might produce:

```
β1 = 120
β2 = −118
```

Huge numbers cancel each other.

This makes the model **unstable**.

Ridge prevents this by shrinking coefficients.

---

# 7. The Bias–Variance Tradeoff

Regularization intentionally introduces a **little bias**.

But it reduces **variance** a lot.

```
High variance → overfitting
High bias → underfitting
```

Ridge moves the model toward the middle.

---

# 8. A Simple Way to Think About It

Imagine you're trying to explain a pattern.

Two explanations:

```
Explanation A:
y = 3x
```

```
Explanation B:
y = 320x − 295x + 2x
```

Both might fit the data.

But explanation A is **simpler and more stable**.

Regularization forces the model to prefer explanations like A.

---

# 9. The Key Idea in One Sentence

Regularization assumes:

> **True relationships in nature are usually simple, not extreme.**

So we penalize models that rely on **huge coefficients**.

---

💡 Since you’re working on ML models for your EMS prediction project, this becomes extremely important because:

- you have **many variables**
    
- many are **correlated clinical measurements**
    
- datasets are **noisy**
    

Regularization keeps the model **stable and generalizable**.
