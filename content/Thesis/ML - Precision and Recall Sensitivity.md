---
share: true
---
2026-03-09  14:39
Tags:[[Technical Literacy|Technical Literacy]]



---

# 1. Start With the Confusion Matrix

![[Pasted image 20260309144006.png|Pasted image 20260309144006.png]]

|Case|Model Prediction|Actual Outcome|
|---|---|---|
|Patient A|High risk|Adverse outcome|
|Patient B|High risk|No event|
|Patient C|Low risk|Adverse outcome|
|Patient D|Low risk|No event|

So we get:

```
TP = predicted event and event happens
FP = predicted event but no event happens
FN = predicted no event but event happens
TN = predicted no event and no event happens
```

---

# 2. Recall (Sensitivity)

Recall answers this question:

> Among all patients who actually had adverse outcomes, how many did the model detect?

Formula:

```
Recall = TP / (TP + FN)
```

Example:

Suppose in your dataset:

```
Total real adverse outcomes = 100
Model detected = 60
Missed = 40
```

Then

```
Recall = 60 / 100 = 0.60
```

Meaning:

> The model catches **60% of dangerous cases**.

---

### Why Recall Matters in Healthcare

Missing a dangerous patient can be very costly.

Example:

```
Patient refuses transport
Model says low risk
Patient deteriorates later
```

So many medical systems prefer:

```
Higher recall
```

Even if it means more false alarms.

---

# 3. Precision

Precision answers a different question:

> Among patients predicted as high risk, how many actually have events?

Formula:

```
Precision = TP / (TP + FP)
```

Example:

Model flags:

```
100 high-risk patients
```

But only:

```
20 actually have adverse outcomes
```

Then

```
Precision = 20 / 100 = 0.20
```

Meaning:

> Only **20% of alerts are real events**.

---

# 4. Why Precision Matters

Too many false alarms can overwhelm the system.

Example EMS scenario:

```
Model flags 500 patients
But only 20 truly deteriorate
```

Clinicians will stop trusting the system.

So precision controls **alert quality**.

---

# 5. Precision vs Recall Trade-off

Usually you cannot maximize both.

Example threshold:

```
Risk > 0.20 → high risk
```

Model flags many patients.

Result:

```
Recall ↑
Precision ↓
```

Lower threshold catches more events but produces more false positives.

---

If you increase threshold:

```
Risk > 0.60 → high risk
```

Now only extreme patients flagged.

Result:

```
Precision ↑
Recall ↓
```

You catch fewer events but alerts are more accurate.

---

# 6. Intuition With Your EMS Project

Imagine:

```
10,000 refusal patients
100 adverse outcomes
```

Model flags **top 500 high-risk patients**.

Among them:

```
50 events
```

Then

```
Precision = 50 / 500 = 10%
Recall = 50 / 100 = 50%
```

Interpretation:

```
Half of dangerous patients are detected
But 90% of alerts are false alarms
```

This is actually **very common in rare event prediction**.

---

# 7. Why Precision/Recall Matters More Than Accuracy

Accuracy:

```
(TP + TN) / Total
```

In rare events this is misleading.

Example:

```
Event rate = 1%
```

If model predicts:

```
No event for everyone
```

Accuracy:

```
99%
```

But recall:

```
0%
```

Model is useless.

---

# 8. Precision-Recall Curve

Instead of picking one threshold, we can evaluate **all thresholds**.

Plot:

```
Recall (x-axis)
Precision (y-axis)
```

This gives a **PR curve**.

Area under this curve:

```
Average Precision
```

This metric is **better than ROC when events are rare**.

Many healthcare ML papers report both.

---

# 9. Relationship With AUC

They measure different things.

|Metric|Meaning|
|---|---|
|AUC|ranking ability|
|Precision|quality of positive predictions|
|Recall|ability to detect events|

So a model can have:

```
Good AUC
Poor precision
```

Especially when events are rare.


---

# 11. A Small Mental Model

Think of it like this:

```
Recall   → How many dangerous patients we catch
Precision → How reliable our alerts are
```

Both matter depending on the **clinical objective**.

---
















```
Recall = Sensitivity
Precision ≠ Specificity
```

So only **one pair is the same**.

---

# 1. Recall = Sensitivity (Correct)

These two are the same metric, just used in different fields.

In **machine learning** we say **Recall**.  
In **medicine** we say **Sensitivity**.

Formula:

[  
Recall = Sensitivity = \frac{TP}{TP + FN}  
]

Meaning:

> Among all real events, how many did we detect?

Example in your EMS model:

If 100 patients truly deteriorate and your model detects 60:

```
Recall / Sensitivity = 60%
```

So:

```
Recall = Sensitivity
```

---

# 2. Specificity (Different from Precision)

Specificity measures something different.

Formula:

[  
Specificity = \frac{TN}{TN + FP}  
]

Meaning:

> Among patients without events, how many did we correctly identify as safe?

Example:

If 9900 patients have no adverse outcome and the model correctly predicts 9800 as safe:

```
Specificity = 9800 / 9900
```

---

# 3. Precision (Different concept)

Precision focuses on the **predicted positives**.

Formula:
$$
[  
Precision = \frac{TP}{TP + FP}  
]
$$
Meaning:

> Among predicted high-risk patients, how many actually have events?

Example:

Model flags 100 high-risk patients.

If 30 actually deteriorate:

 
Precision = 30 / 100 = 30%


# 4. Visual Comparison (Very Helpful)

|Metric|Formula|Question it answers|
|---|---|---|
|Sensitivity / Recall|TP / (TP + FN)|Did we catch the events?|
|Specificity|TN / (TN + FP)|Did we correctly identify safe patients?|
|Precision|TP / (TP + FP)|Are our alerts correct?|

---

# 5. Why Precision and Specificity Feel Similar

They both involve **false positives**, which causes confusion.

But they answer different questions.

Specificity asks:

```
Among actual negatives, how many are correctly predicted?
```

Precision asks:

```
Among predicted positives, how many are correct?
```

Different denominators.

---

# 6. Simple EMS Example

Imagine:

```
10,000 refusal patients
100 adverse outcomes
```

Model results:

```
TP = 50
FP = 150
FN = 50
TN = 9750
```

Now compute:

Recall / Sensitivity:

```
50 / (50 + 50) = 50%
```

Specificity:

```
9750 / (9750 + 150) ≈ 98.5%
```

Precision:

```
50 / (50 + 150) = 25%
```

Interpretation:

- Model catches **half the dangerous patients**
    
- Correctly identifies **almost all safe patients**
    
- Only **25% of alerts are real**
    

This pattern is **very common in rare-event prediction**.

---

# 7. The Key Mental Model

Think of it like this:

```
Sensitivity / Recall → detect dangerous patients

Specificity → identify safe patients

Precision → how trustworthy our alerts are
```

Each metric answers a **different clinical question**.

---

# 8. One Small Trick to Remember

Look at the denominator.

Recall / Sensitivity:

```
TP + FN
```

→ all **actual positives**

Precision:

```
TP + FP
```

→ all **predicted positives**

Specificity:

```
TN + FP
```

→ all **actual negatives**

---

