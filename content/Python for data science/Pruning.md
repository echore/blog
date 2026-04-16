---
share: true
---
2026-04-16  11:21
Tags:

---

# 🌳 1. What is pruning (intuitive)?

👉 Pruning = **cutting unnecessary branches of the tree**

Think:

> A decision tree is like a very overthinking person  
> → keeps asking more and more specific questions  
> → eventually becomes ridiculous

Example:

```text
IF age > 65
  AND SpO2 < 94
  AND heart rate = 103
  AND day = Tuesday
```

😅 That last condition is probably useless.

👉 Pruning = **remove those useless splits**

---

# 🧠 2. Why do we need pruning?

Because of **overfitting**.

Without pruning:

- Tree memorizes training data
    
- Performs badly on new data
    

---

### Mental model

|Tree type|Behavior|
|---|---|
|Too big ❌|memorizes noise|
|Pruned ✅|captures real patterns|

---

# ✂️ 3. Two types of pruning (very important)

## (1) Pre-pruning (early stopping)

👉 Stop the tree from growing too much

You already used this without realizing:

```python
max_depth=5
min_samples_leaf=10
```

These are **pre-pruning controls**

---

### Think of it like:

> “Don’t let the tree become too detailed in the first place”

---

## (2) Post-pruning (the real “pruning”)

👉 Grow full tree first → then cut it back

This is more “theoretical correct” way.

---

# 🔪 4. Core idea of post-pruning

👉 Ask:

> “If I remove this split, does performance get worse?”

If NOT → remove it

---

### Example

Before:

```text
Split A
 ├── Split B
 │     ├── Leaf (pure)
 │     └── Leaf (pure)
```

After pruning:

```text
Split A
 └── Leaf (still good enough)
```

👉 If removing B doesn't hurt much → cut it

---

# ⚖️ 5. Cost-complexity pruning (the only concept you need)

In sklearn, pruning is based on:

> Balance between:

- model accuracy
    
- model simplicity
    

---

### Formula intuition (no need to memorize)

```
Total Loss = Error + α × Tree Complexity
```

- Error ↓ → better fit
    
- Complexity ↑ → more splits
    

👉 α (ccp_alpha) controls trade-off

---

### Key idea:

|α value|Effect|
|---|---|
|small α|big tree|
|large α|more pruning|

---

