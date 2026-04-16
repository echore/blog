---
share: true
---
2026-04-16  11:31
Tags:

---

# 🧠 1. What is Gini impurity (intuition)?

👉 Gini impurity measures:

> **“How mixed a group is”**

---

### Think like this:

You randomly pick one sample from a group.

👉 Gini = probability that you **misclassify it**

---

### Examples

#### Case 1: perfectly pure

```text
[Fraud, Fraud, Fraud, Fraud]
```

👉 Gini = 0  
✔️ no confusion  
✔️ perfect

---

#### Case 2: very mixed

```text
[Fraud, Legit, Fraud, Legit]
```

👉 Gini = high (~0.5)  
❌ very confusing

---

👉 So:

|Situation|Gini|
|---|---|
|pure|0|
|mixed|high|

---

# 🔢 2. The formula 

![[Pasted image 20260416113608.png|Pasted image 20260416113608.png]]


![[Pasted image 20260416113639.png|Pasted image 20260416113639.png]]

---

**We want to minimize the gini impurity in the leaf node**

