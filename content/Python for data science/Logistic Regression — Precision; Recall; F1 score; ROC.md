---
share: true
---
2026-03-26  11:22
Tags:

---

# 0. First: What problem are we solving?

We’re in **binary classification**:

- Predict: 0 or 1
    
- Example:
    
    - Disease prediction (yes/no)
        
    - Fraud detection (fraud/not)
        

But your model is **not perfect**, so predictions fall into 4 cases:

![[Pasted image 20260326113010.png|Pasted image 20260326113010.png]]
👉 This table = **confusion matrix**

---

# 1. Precision

### Definition
$$
[  
\text{Precision} = \frac{TP}{TP + FP}  
]
$$
### Intuition

> “When I say YES, how often am I correct?”
> sensitity

---

### Example (medical)

You predict 100 people have disease:

- 80 actually have it → TP
    
- 20 don’t → FP
    

👉 Precision = 80 / (80+20) = 0.8

---

### Mental model

Precision = **don’t cry wolf**

- High precision → few false alarms
    
- Important when:
    
    - fraud detection
        
    - spam filtering
        

---

# 2. Recall 

### Definition
$$
[  
\text{Recall} = \frac{TP}{TP + FN}  
]
$$
### Intuition

> “Out of all real positives, how many did I catch?”

---

### Example (same case)

There are actually 200 sick people:

- You found 80 → TP
    
- Missed 120 → FN
    

👉 Recall = 80 / (80+120) = 0.4

---

### Mental model

Recall = **don’t miss important cases**

- High recall → few missed positives
    
- Important when:
    
    - disease detection
        
    - cancer screening
        

---

# 3. Precision vs Recall (core trade-off)

This is **THE key idea**.

👉 You can’t maximize both easily.

---

### In ML terms

You control this via:

👉 **decision threshold**

Example:

```python
model.predict_proba(X)
```

- threshold = 0.5 → default
    
- threshold ↓ → more positives → ↑ recall, ↓ precision
    
- threshold ↑ → fewer positives → ↑ precision, ↓ recall
    

---

# 4. F1 Score (balance between them)

### Definition
$$
[  
F1 = 2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}  
]
$$
---

### Why not just average?

Because F1 is **harmonic mean**:

👉 punishes imbalance

---

### Example

|Precision|Recall|F1|
|---|---|---|
|0.9|0.1|low|
|0.6|0.6|higher|

👉 F1 says:

> “You must be good at BOTH”

---

### When to use F1?

- imbalanced data
    
- when both FP and FN matter
    

---

# 5. ROC Curve (this is where it gets interesting)

Now we move from **single threshold → all thresholds**

---

## Key idea

Instead of fixing threshold = 0.5

👉 try ALL thresholds

---

### ROC curve plots:

- X-axis: **False Positive Rate (FPR)**  
- $$
    [  
    FPR = \frac{FP}{FP + TN}  
    ]
    $$
- Y-axis: **True Positive Rate (Recall)**  
- $$
    [  
    TPR = Recall  
    ]
    $$

---

### Interpretation

Each point = a threshold

---

### Visual intuition

- Top-left = best
    
- Diagonal = random guessing
    

---

# 6. AUC (Area Under Curve)

### Definition

Area under ROC curve

---

### Meaning

> Probability that model ranks a random positive higher than a random negative

---

### Values

|AUC|Meaning|
|---|---|
|0.5|random|
|0.7|decent|
|0.8|good|
|0.9|strong|

---

# 7. When to use what (this is what interviewers LOVE)

## If dataset is balanced:

- Accuracy OK
    
- ROC-AUC useful
    

---

## If dataset is imbalanced (VERY common)

Example: fraud = 1%

👉 Accuracy is useless

---

### Use:

- Precision
    
- Recall
    
- F1
    
- PR curve (even better than ROC sometimes)
    
