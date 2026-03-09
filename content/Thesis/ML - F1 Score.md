---
share: true
---
2026-03-09  14:41
Tags:[[Technical Literacy|Technical Literacy]]

Great — **F1 score** is the natural next step after **precision and recall**, because it answers a practical question:

> _If a model has both precision and recall, how do we summarize them in one number?_

Let’s go step by step.

---

# 1. Quick Recap: Precision and Recall

From earlier:

**Precision**

> Among predicted positives, how many are correct?

$$

[  
Precision = \frac{TP}{TP + FP}  
]
$$
**Recall (Sensitivity)**

> Among real positives, how many did we detect?
$$
[  
Recall = \frac{TP}{TP + FN}  
]
$$
Example for your **EMS adverse outcome prediction**:

||Actual Event|No Event|
|---|---|---|
|Predicted Event|30|70|
|Predicted No Event|20|9880|

So:

```
TP = 30
FP = 70
FN = 20
TN = 9880
```

Precision:

```
30 / (30 + 70) = 0.30
```

Recall:

```
30 / (30 + 20) = 0.60
```

Meaning:

- 30% of alerts are real events
    
- 60% of real events are caught
    

---

# 2. Why We Need F1 Score

Suppose two models:

|Model|Precision|Recall|
|---|---|---|
|Model A|0.80|0.30|
|Model B|0.40|0.60|

Which one is better?

Hard to say:

- Model A → very accurate alerts but misses many events
    
- Model B → catches more events but many false alarms
    

So we combine them into one metric.

---

# 3. Definition of F1 Score

F1 score is the **harmonic mean** of precision and recall.

Formula:
$$
[  
F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}  
]
$$
Important: it is **not a normal average**.

The harmonic mean punishes imbalance.

---

# 4. Example Calculation

Using the EMS example:

```
Precision = 0.30
Recall = 0.60
```

F1:

```
2 × (0.30 × 0.60) / (0.30 + 0.60)
= 0.36 / 0.90
= 0.40
```

So:

```
F1 = 0.40
```

---

# 5. Why Harmonic Mean?

The harmonic mean prevents cheating.

Example:

|Precision|Recall|F1|
|---|---|---|
|0.90|0.10|0.18|
|0.60|0.60|0.60|

Even though the first model has **very high precision**, the terrible recall causes F1 to be low.

F1 prefers **balanced performance**.

---

# 6. Intuition

Think of it this way:

```
Precision = alert quality
Recall = event coverage
F1 = balance between them
```

Or:

```
Precision → how many alerts are correct
Recall → how many real events we catch
F1 → overall detection quality
```

---

# 7. When F1 Is Useful

F1 is especially useful when:

- classes are **imbalanced**
    
- both false positives and false negatives matter
    

Example situations:

- fraud detection
    
- medical alerts
    
- anomaly detection
    

Your EMS model fits this category.

---

# 8. When F1 Is NOT Ideal

F1 ignores **true negatives**.

So in highly imbalanced datasets:

```
TN = very large
```

F1 does not consider them.

That’s why medical papers often prioritize:

```
AUC
Calibration
```

instead of F1.

---

# 9. Relationship Between Metrics

Think of metrics like this:

```
Accuracy → overall correctness
AUC → ranking ability
Precision → alert quality
Recall → event detection
F1 → balance of precision & recall
Calibration → probability reliability
Lift → risk concentration
```

Each answers a **different question**.

---

# 10. Example Interpretation for Your EMS Project

Suppose your model reports:

```
AUC = 0.74
Precision = 0.18
Recall = 0.52
F1 = 0.27
```

Interpretation:

- model moderately separates high-risk patients
    
- catches about half of adverse events
    
- alerts have low precision due to rare outcomes
    

That would be **completely normal for healthcare prediction**.

---

# 12. A Small But Important Insight

In rare-event prediction like EMS:

```
Precision will often be low
```

Even with good models.

Example:

```
event rate = 1%
```

Even a strong model might only achieve:

```
Precision = 10–20%
```

That’s actually **expected**.

---

