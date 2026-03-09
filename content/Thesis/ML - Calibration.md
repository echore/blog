---
share: true
---
2026-03-09  14:23
Tags:[[Technical Literacy|Technical Literacy]]


---

# 1. First: What Calibration Means

Calibration answers this question:

> **Are the predicted probabilities actually correct?**

Example.

Your model predicts:

|Patient|Predicted Risk|
|---|---|
|A|0.80|
|B|0.80|
|C|0.80|
|D|0.80|
|E|0.80|

If the model is **well calibrated**, then among patients with **0.80 predicted risk**, about **80% should actually experience the outcome**.

So:

```text
Predicted probability ≈ Real probability
```

That is **calibration**.

---

# 2. Why Calibration Matters in Medicine

In healthcare, decisions are often **threshold-based**.

Example:

```
Risk > 20% → send follow-up team
Risk > 50% → hospital admission
```

If your model predicts:

```
Risk = 60%
```

But the real probability is **20%**, the model is **dangerously overconfident**.

So in clinical settings:

```
Calibration is often more important than AUC
```

Because clinicians rely on **the actual probability**.

---

# 3. Discrimination vs Calibration

This distinction is very important.

|Metric|What it measures|
|---|---|
|**AUC**|ranking ability|
|**Calibration**|probability accuracy|

Example:

Model prediction:

|Patient|Risk|Outcome|
|---|---|---|
|A|0.90|yes|
|B|0.80|yes|
|C|0.40|no|
|D|0.20|no|

Perfect ranking → **high AUC**

But imagine the real event rate is:

```
A = yes
B = no
C = no
D = no
```

Now:

```
Predicted: 90%
Actual: maybe 25%
```

Ranking still decent → **AUC ok**

But probability **wrong** → **poor calibration**

---

# 4. Calibration Curve (the most common visualization)

The most common way to check calibration is a **calibration plot**.

Idea:

1. Divide predictions into groups
    
2. Compare predicted vs actual risk
    

Example:

|Predicted Risk|Actual Event Rate|
|---|---|
|0.1|0.09|
|0.2|0.18|
|0.4|0.35|
|0.6|0.50|
|0.8|0.65|

Then plot:

```
x-axis: predicted probability
y-axis: observed probability
```

If the model is perfect:

```
points fall on a diagonal line
```

```
Observed
   |
1.0|          *
   |       *
   |    *
   | *
0.0+----------------
   0      Predicted
```

That diagonal is called the **perfect calibration line**.

---

# 5. Overconfidence vs Underconfidence

Calibration plots reveal **two common problems**.

### Overconfident model

Model predicts too high.

Example:

|Predicted|Actual|
|---|---|
|0.8|0.5|

Meaning:

```
Model exaggerates risk
```

---

### Underconfident model

Model predicts too low.

Example:

|Predicted|Actual|
|---|---|
|0.3|0.5|

Meaning:

```
Model underestimates risk
```

---

# 6. Calibration Metrics

Some numerical metrics measure calibration.

### Brier Score

Most common.

Formula idea:

```
(predicted probability − actual outcome)^2
```

Example:

Prediction = 0.8  
Outcome = 1

```
(0.8 - 1)^2 = 0.04
```

Prediction = 0.8  
Outcome = 0

```
(0.8 - 0)^2 = 0.64
```

Then average over all cases.

Lower = better.

---

### Calibration slope

Used often in medical ML.

Interpretation:

|slope|meaning|
|---|---|
|1|perfect|
|<1|predictions too extreme|
|>1|predictions too conservative|

---

# 7. Why Models Often Need Calibration

Many ML models are **not naturally calibrated**.

Examples:

Poor calibration:

- Random Forest
    
- Gradient Boosting
    
- Neural Networks
    

Better calibration:

- Logistic regression
    

Because logistic regression models **probability directly**.

---

# 8. Calibration Methods

Two common fixes.

### Platt Scaling

Fits a logistic regression to the predictions.

```
predicted_score → calibrated_probability
```

---

### Isotonic Regression

Non-parametric calibration.

More flexible but needs more data.


---

# 10. One very important idea (clinicians care about this)

Think of model evaluation like this:

```
AUC → Can we rank patients correctly?

Calibration → Are the predicted risks trustworthy?
```

Or more simply:

```
AUC  = who is higher risk
Calibration = how risky exactly
```

---

# 11. Final intuition

Imagine a **weather forecast**.

Prediction:

```
Rain probability = 70%
```

If over 100 days with 70% prediction:

```
Rain occurs ~70 times
```

Then the weather model is **well calibrated**.

If rain only happens **30 times**, the model is **miscalibrated**.

---











Ranking still decent → AUC ok

But probability wrong → poor calibration why this would heappen?


---

# 1. AUC Only Cares About Order

Remember what **AUC really measures**:

> If we randomly choose one positive case and one negative case, what is the probability the model ranks the positive one higher?

Notice something important:

```text
AUC only cares about ranking
NOT the actual probability values
```

Example:

|Patient|Predicted Risk|Outcome|
|---|---|---|
|A|0.90|event|
|B|0.80|event|
|C|0.40|no event|
|D|0.20|no event|

Perfect ranking:

```text
event patients > non-event patients
```

So **AUC ≈ 1.0**

---

# 2. But Calibration Cares About Probability

Calibration asks a different question:

> If we predict **80% risk**, do about **80% actually have the event?**

Now imagine the **true event rate is much lower**.

Real outcomes:

|Patient|Predicted|Outcome|
|---|---|---|
|A|0.90|event|
|B|0.80|no event|
|C|0.40|no event|
|D|0.20|no event|

Ranking is still correct enough:

```text
0.9 > 0.8 > 0.4 > 0.2
```

So **AUC stays decent**.

But predicted probabilities are **too high**.

Example:

```text
Predicted: 90%
Real: maybe 20–30%
```

So **calibration is bad**.

---

# 3. Key Insight

AUC depends only on **relative order**.

Calibration depends on **absolute probability values**.

Think of it like this.

### Model A

|Risk score|
|---|
|0.90|
|0.80|
|0.40|
|0.20|

### Model B

|Risk score|
|---|
|9|
|8|
|4|
|2|

Both models produce the **same ranking**.

So:

```text
AUC = identical
```

But Model B’s numbers **aren't probabilities at all**.

So calibration is meaningless.

---

# 4. Another Intuition (Scaling Problem)

Imagine the model outputs:

True probabilities should be:

```text
0.10
0.08
0.04
0.02
```

But the model predicts:

```text
0.90
0.80
0.40
0.20
```

Every probability is **9× too big**.

Ranking stays perfect → **AUC unchanged**.

But probabilities are wrong → **calibration terrible**.

---

# 5. Why This Happens in Practice

Several reasons.

### 1️⃣ Overfitting

Complex models may exaggerate probabilities.

Example models:

- Random Forest
    
- Gradient Boosting
    
- Neural networks
    

They often produce **overconfident predictions**.

---

### 2️⃣ Class imbalance

Your EMS dataset likely has **rare adverse events**.

Example:

```text
event rate = 2%
```

Models often inflate probabilities for rare events.

---

### 3️⃣ Dataset shift

If training data ≠ real-world data:

Probability estimates drift.

Ranking may still work.

---

### 4️⃣ Score ≠ probability

Some models produce **scores**, not calibrated probabilities.

Examples:

- SVM decision function
    
- boosted trees
    

They need **calibration afterwards**.

---

# 6. Visual Example

Imagine ranking patients from lowest risk to highest risk.

```text
True risk:
1% → 2% → 3% → 4%
```

Model prediction:

```text
10% → 20% → 30% → 40%
```

Ordering is perfect.

So:

```text
AUC = excellent
```

But:

```text
probabilities are 10x too big
```

So:

```text
Calibration = bad
```

---

# 7. Why This Matters

Imagine your model predicts:

```text
Risk = 60%
```

But the real risk is:

```text
10%
```

A clinician might think:

> This patient is extremely dangerous.

But actually the risk is moderate.

So **clinical decisions could be wrong**.

This is why **medical ML papers almost always report calibration**.

---
