---
share: true
---
2026-03-09  17:19
Tags:

---

# 1️⃣ The core question

When we train a model, there are **two ways it can go wrong**:

1. The model is **too simple** → cannot capture the real pattern
    
2. The model is **too sensitive to the training data**
    

These correspond to:

|Problem|Name|
|---|---|
|model too simple|**High Bias**|
|model too sensitive|**High Variance**|

---

# 2️⃣ Bias (underfitting)

Bias means:

> The model makes **systematic mistakes** because it is too simple.

Example:

Imagine the real relationship is curved:

```
true pattern
   *
 *   *
*     *
 *   *
   *
```

But the model forces a straight line:

```
---------
```

Even with infinite data, the model **cannot represent the pattern**.

This is **high bias**.

Typical symptoms:

```
train error → high
test error → high
```

Example models with high bias:

- linear regression on nonlinear data
    
- polynomial degree = 1
    
- very strong regularization
    

---

# 3️⃣ Variance (overfitting)

Variance means:

> The model changes a lot depending on the training data.

Example:

Two slightly different training sets produce very different models.

Example shapes:

```
model 1
~\/\_/\/~

model 2
_/\/\/\/_
```

The model is **too flexible** and memorizes noise.

Symptoms:

```
train error → very low
test error → high
```

Typical high variance models:

- high-degree polynomial
    
- deep decision trees
    
- neural networks with little regularization
    

---

# 4️⃣ Visualization

The classic diagram looks like this:

```
Error
  ^
  |\
  | \
  |  \        test error
  |   \___/\____
  |       \
  |        \ train error
  |
  +------------------------>
       model complexity
```

Left side:

```
model too simple
high bias
```

Right side:

```
model too complex
high variance
```

The sweet spot is **in the middle**.

---

# 5️⃣ The mathematical idea

Total prediction error can be thought of as:

[  
\text{Error} =  
Bias^2 + Variance + Noise  
]

Meaning:

```
Total error =
model wrong assumptions
+ model instability
+ irreducible randomness
```

Noise cannot be reduced.

So ML tries to balance:

```
bias
variance
```

---

# 6️⃣ Example with polynomial regression

You already saw this in your notebook.

### Degree = 1

```
y = β0 + β1x
```

Model too simple.

```
high bias
low variance
```

---

### Degree = 10

```
y = β0 + β1x + β2x² + ... + β10x¹⁰
```

Model very flexible.

```
low bias
high variance
```

---

### Degree = 3

Good balance.

```
moderate bias
moderate variance
```

---

# 7️⃣ Dartboard intuition (classic example)

Imagine predicting the center of a dartboard.

### High bias

All darts land **far from center** but clustered.

```
oooo
oooo
```

Model is consistently wrong.

---

### High variance

Darts spread everywhere.

```
o   o
  o
o    o
```

Model unstable.

---

### Ideal

```
  o
 ooo
  o
```

Low bias and low variance.

---

# 8️⃣ How regularization affects bias and variance

Regularization intentionally increases bias to reduce variance.

Example:

Without regularization:

```
model too flexible
variance high
```

With LASSO / Ridge:

```
model simplified
variance ↓
bias slightly ↑
```

But total error ↓.

---

# 9️⃣ Why cross validation helps

Cross validation helps us **detect variance problems**.

If model performance varies a lot across folds:

```
variance high
```

If performance is stable:

```
variance low
```

So CV helps us choose the model complexity that balances bias and variance.

---

# 🔟 Model examples

Here is how common models behave:

|Model|Bias|Variance|
|---|---|---|
|Linear regression|high|low|
|Ridge / LASSO|medium|medium|
|Decision tree|low|high|
|Random forest|medium|low|
|Neural networks|low|high|

---

# 1️⃣1️⃣ Why this matters for your EMS project

Your dataset likely has:

```
many predictors
limited events
```

That situation tends to cause:

```
high variance
```

Because the model can memorize noise.

Solutions:

```
regularization
feature selection
cross validation
simpler models
```

Exactly the techniques you’re learning.

---

# 1️⃣2️⃣ The deep intuition

Machine learning is basically this game:

> Make the model **flexible enough to learn patterns**, but **not flexible enough to memorize noise**.

Every technique you’ve learned relates to this balance:

|Technique|Purpose|
|---|---|
|polynomial features|reduce bias|
|regularization|reduce variance|
|cross validation|measure variance|
|feature selection|reduce variance|

---

✅ If you'd like, the **next concept that connects everything you've learned** is something many people in ML don't fully understand:

**Why tree models (Random Forest, XGBoost) often outperform linear models even when linear models seem theoretically correct.**

And that insight actually explains **a lot about real-world prediction problems like healthcare data.**