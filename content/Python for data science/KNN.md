---
share: true
---
2026-04-02  10:34
Tags:

---

# 1. Core Idea (super intuitive)

Imagine this:

> You move to a new city. You don’t know what a neighborhood is like.  
> What do you do? You look at the **people living nearby**.

KNN does exactly that.

**Definition:**

> To predict something about a new data point, KNN looks at the **k closest data points** and uses their labels.

---

# 2. The Algorithm (what actually happens)

Let’s say you want to classify whether a patient is “high-risk” or “low-risk”.

### Step-by-step:

1. Choose a number **k** (e.g., k = 3)
    
2. For a new patient:
    
    - Compute distance to all training patients
        
3. Find the **k closest ones**
    
4. Look at their labels:
    
    - Majority vote → classification
        
    - Average → regression
        

---

# 3. Distance = the heart of KNN

This is where most people don’t _really_ understand KNN.

KNN depends entirely on **how you measure “closeness”**.

### Most common: Euclidean distance
$$
[  
d = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}  
]
$$
Think:

> “straight-line distance in space”

---

### Why scaling matters (VERY IMPORTANT)

If one feature is huge (e.g., income = 100,000) and another small (age = 20),  
distance gets dominated by the big one.

So we usually do:

- Standardization (mean=0, std=1)
    

---

# 4. Choosing k (this is where the magic is)

Think of **k as bias vs variance control**:

### Small k (e.g., k=1)

- Very sensitive
    
- Overfits (noise matters too much)
    

### Large k (e.g., k=50)

- Smooth decision
    
- May underfit (lose local patterns)
    

---

### Intuition:

- Small k → “trust your closest neighbor”
    
- Large k → “trust the crowd”
    

---

# 5. What KNN is REALLY doing (deep intuition)

This is the part most courses skip.

KNN is basically:

> “Instead of learning a model, I store the data and decide later.”

So:

- No training phase (lazy learner)
    
- All computation happens at prediction time
    

---

### Compare to logistic regression:

|Model|What it does|
|---|---|
|Logistic Regression|Learns a global boundary|
|KNN|Makes local decisions|

---

# 6. Decision Boundary (important insight)

KNN creates **non-linear boundaries** naturally.

Why?

Because:

- Each prediction depends on local neighbors
    
- Different regions → different decisions
    

So even without complex math, it can capture complex patterns.

---

# 7. Classification vs Regression

### Classification:

- Majority vote
    

### Regression:

- Average of neighbors
    

Example:

- Neighbors’ house prices = [200k, 220k, 250k]  
    → prediction = ~223k
    

---

# 8. Strengths (why people use KNN)

- Simple
    
- No assumptions about data
    
- Works well for small datasets
    
- Captures non-linear patterns
    

---

# 9. Weaknesses (VERY important for real-world use)

### 1. Slow at prediction

Because:

- Must compute distance to ALL points
    

### 2. Curse of dimensionality

As features increase:

- Everything becomes “equally far”
    

So KNN breaks down in high dimensions (very relevant for your 491 variables project)

---

### 3. Sensitive to noise

One bad neighbor → wrong prediction

---



![[Pasted image 20260402103903.png|Pasted image 20260402103903.png]]

---

# 1. What is a “tie” in KNN?

Imagine:

- k = 4
    
- Your 4 nearest neighbors are:
    

```
Class A, Class A, Class B, Class B
```

Now:

- A = 2 votes
    
- B = 2 votes
    

→ **tie**

So the model literally gets stuck:

> “I don’t know which class to pick.”

---

# 2. “Always choose an odd K” — why?

This is the simplest trick.

If:

- k = 3 → votes like (2 vs 1) → no tie
    
- k = 5 → (3 vs 2) → no tie
    

So:

> Odd K reduces the chance of ties (especially in binary classification)

---

### BUT think deeper (important)

This only works well when:

- You have **2 classes**
    

If you have:

- 3+ classes → ties can still happen even with odd K
    

---

# 3. “Reduce K by 1 until tie is broken”

This is a **deterministic strategy**.

Example:

```
k = 4 → tie
k = 3 → no tie
```

So you're basically saying:

> “If the crowd is confusing, listen to fewer people.”

---

### Think critically:

This means:

- You are changing the model **dynamically per prediction**
    
- That’s a bit hacky but practical
    

---

# 4. “Randomly break tie”

This is:

> “Flip a coin”

---

### When is this okay?

- When ties are rare
    
- When dataset is large
    

---

### Problem:

- Not reproducible
    
- Two runs → different results
    

Bad for:

- Medical models (like your EMS project)
    
- Anything high-stakes
    

---

# 5. “Choose nearest class point” (this one is subtle and important)

This is actually the **most meaningful strategy**.

Instead of:

> “Who has more votes?”

You ask:

> “Who is closest to me?”

---

### Example:

Neighbors:

|Distance|Class|
|---|---|
|0.1|A|
|0.2|B|
|0.3|B|
|0.4|A|

Votes:

- A = 2
    
- B = 2 → tie
    

BUT:

- Closest point = Class A (distance 0.1)
    

→ choose **A**

---

### This leads to a deeper concept:

You’re implicitly doing:

> **distance-weighted KNN**

---

# 6. Big insight (this is the real takeaway)

All these methods are trying to answer:

> “When local information is ambiguous, what should we trust?”

|Method|Philosophy|
|---|---|
|Odd K|Avoid ambiguity|
|Reduce K|Trust smaller neighborhood|
|Random|Accept uncertainty|
|Nearest point|Trust strongest signal|

---

# 7. What would YOU use (real-world thinking)

For your type of work (medical risk prediction):

You should **NOT use random**.

Better choices:

1. Distance-weighted KNN
    
2. Or just avoid tie by choosing good K via CV
    

---
