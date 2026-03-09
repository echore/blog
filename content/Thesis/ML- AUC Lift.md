---
share: true
---
2026-03-09  14:18
Tags:[[Technical Literacy|Technical Literacy]]


---

# 1. First: What problem are AUC and Lift solving?

In your project, the model predicts something like:

> **Will a patient have an adverse outcome after refusing transport?**

So the model outputs something like:

|Patient|Predicted Risk|
|---|---|
|A|0.92|
|B|0.74|
|C|0.51|
|D|0.30|
|E|0.10|

This is **not a yes/no answer**.  
It’s a **probability ranking**.

So the question becomes:

**How good is the ranking?**

Two common ways to evaluate this are:

- **AUC**
    
- **Lift**
    

They measure **different things**.

---

# 2. AUC (Area Under the Curve)

AUC comes from the **ROC curve**.

But let’s skip the math first and understand the intuition.

### Intuition

AUC answers this question:

> If I randomly pick **one positive case** and **one negative case**,  
> what is the probability the model ranks the positive case higher?

Example:

True outcomes:

|Patient|True Outcome|
|---|---|
|A|adverse|
|B|adverse|
|C|no event|
|D|no event|

Model prediction:

|Patient|Risk|
|---|---|
|A|0.90|
|B|0.80|
|C|0.40|
|D|0.20|

The model ranked both adverse cases above non-adverse ones.

So performance is excellent.

AUC ≈ **1.0**

---

### Interpretation

| AUC | Meaning         |
| --- | --------------- |
| 0.5 | random guessing |
| 0.6 | weak            |
| 0.7 | acceptable      |
| 0.8 | good            |
| 0.9 | excellent       |

So if your EMS model has:

```
AUC = 0.74
```

You can say:

> The model has **acceptable discrimination ability**.

---

### What AUC really measures

**Discrimination**

Meaning:

> Can the model distinguish high-risk patients from low-risk patients?

It does **NOT** measure:

- calibration
    
- clinical usefulness
    
- how many cases we catch
    

---

# 3. ROC Curve (very briefly)

The ROC curve plots:

```
True Positive Rate (Sensitivity)
vs
False Positive Rate
```

For different thresholds.

Example thresholds:

```
Risk > 0.2 → classify positive
Risk > 0.4 → classify positive
Risk > 0.6 → classify positive
```

Each threshold produces a point.

The **area under this curve = AUC**.

---

# 4. Lift (very important for real-world prediction)

Lift answers a **completely different question**.

Instead of discrimination, it asks:

> If we focus on the **highest-risk patients**, how much better do we perform compared to random selection?

This is extremely important in **risk stratification**.

---

### Example

Imagine:

Population: **10,000 EMS refusals**

True adverse outcomes: **100**

So baseline rate:

```
100 / 10,000 = 1%
```

Randomly selecting patients gives:

```
1% event rate
```

---

### Now suppose the model ranks patients.

We look at the **top 10% highest risk patients**.

That’s **1000 patients**.

Among them we find:

```
40 adverse outcomes
```

So event rate becomes:

```
40 / 1000 = 4%
```

Baseline rate = 1%

Model rate = 4%

Lift =

```
4 / 1 = 4
```

So:

> Lift = **4**

Meaning:

> The top 10% predicted risk group contains **4x more events than random selection**.

---

# 5. Why Lift is very useful in healthcare prediction

In real systems, we often want to:

- target **high-risk patients**
    
- allocate **limited resources**
    

Example:

EMS could flag:

```
Top 5% predicted risk
```

Then paramedics or follow-up teams focus on those patients.

Lift tells you:

> How concentrated the risk is in that top group.

---

# 6. Why your AUC decreased but Lift increased

You mentioned:

> after adding clinical features  
> **AUC decreased but Lift increased**

This actually happens often.

Why?

Because:

AUC measures **overall ranking quality across all patients**

Lift focuses on **the extreme high-risk group**.

Example:

Model A

```
AUC = 0.76
Lift@10% = 3
```

Model B

```
AUC = 0.73
Lift@10% = 5
```

Model B is **better at identifying the highest-risk patients**, even if global ranking is slightly worse.

In **clinical triage systems**, people often prefer:

```
Higher Lift
```


---

# 8. Quick visual summary

Think of it like this:

```
AUC  → how well the model ranks everyone

Lift → how powerful the top-risk group is
```

or

```
AUC  = discrimination
Lift = risk concentration
```

---

