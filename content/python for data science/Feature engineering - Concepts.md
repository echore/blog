---
share: true
---
2026-03-12  14:27
Tags:

---

# 1. What is Feature Engineering?

**Feature engineering = transforming raw data into better inputs for a model.**

Think of it like cooking.

Raw ingredients → vegetables, meat, spices  
Cooked dish → something useful

Machine learning is the same:

Raw data → messy variables  
Features → useful signals for the model

Example:

Raw data

|pulse|systolic_bp|
|---|---|
|120|90|

Instead of giving these directly to the model, we create a **better feature**:

Shock Index:
$$
[  
shock_index = \frac{pulse}{systolic_bp}  
]
$$
Now the model sees a **medical signal**, not just two numbers.

This is feature engineering.

---

# 2. Why Feature Engineering Matters

A famous ML saying:

> **Better data beats better algorithms.**

Why?

Most algorithms are mathematically similar.  
What makes models powerful is **what information you feed them**.

Example:

Predict hospital mortality.

Bad features:

```
patient_id
hospital_room
visit_number
```

Good features:

```
age
shock_index
oxygen_saturation
history_of_cardiac_disease
```

Same model, **totally different performance**.

---

# 3. Common Types of Feature Engineering

Let’s go through the major types.

---

# 3.1 Creating New Features

This is the **most powerful technique**.

Example:

You did something similar already:

```
shock_index = pulse / systolic_bp
pulse_pressure = systolic_bp - diastolic_bp
```

Why useful?

Because medical knowledge says:

- high shock index → possible shock
    
- low pulse pressure → cardiac issues
    

You encode **domain knowledge into numbers**.

This is why doctors + ML works well.

---

# 3.2 Handling Missing Values

Real data always has missing values.

Example

|pulse|BP|
|---|---|
|90|NA|

Options:

### Method 1 — Fill with mean

```
pulse_mean = mean(pulse)
```

### Method 2 — Fill with median

More robust.

### Method 3 — Add missing indicator

Very important.

Example:

```
pulse_missing = 1 if pulse is NA else 0
```

Why?

Sometimes **missingness itself is informative**.

Example:

If a test wasn't taken → patient might not be severe.

---

# 3.3 Encoding Categorical Variables

Models only understand numbers.

Example:

```
gender = male/female
```

Convert to numbers:

```
male = 1
female = 0
```

Better method:

**One-hot encoding**

```
gender_male
gender_female
```

Example:

|gender_male|gender_female|
|---|---|
|1|0|
|0|1|

In Python:

```python
pd.get_dummies(data)
```

or

```python
OneHotEncoder()
```

---

# 3.4 Scaling Features

Many ML models require features on the same scale.

Example:

|feature|value|
|---|---|
|age|70|
|income|100000|

The model thinks income is **more important** just because it's larger.

Scaling fixes this.

### Standardization

[  
x_{scaled} = \frac{x - \mu}{\sigma}  
]

Mean = 0  
Std = 1

Python:

```python
StandardScaler()
```

Needed for:

- Logistic regression
    
- Ridge/Lasso
    
- Neural networks
    
- SVM
    

---

# 3.5 Binning

Convert continuous variable → groups.

Example:

```
age → age_group
```

```
0–18
18–40
40–65
65+
```

Why?

Some relationships are **non-linear**.

Example:

Risk may jump sharply after age 65.

---

# 3.6 Interaction Features

Sometimes variables **interact**.

Example:

```
smoking * age
```

Meaning:

Smoking is more dangerous for older patients.

Example:

```
risk = smoking × age
```

Python:

```python
PolynomialFeatures()
```

This creates

```
x
x^2
x*y
```

---

# 3.7 Feature Selection

Not all features are useful.

Example:

491 variables → many are useless.

We remove:

- near-zero variance features
    
- duplicates
    
- leakage variables
    
- highly correlated features
    

Then methods like:

- **LASSO**
    
- **Random Forest importance**
    

help select the best predictors.

You actually already did this.

---

# 4. Feature Engineering vs Feature Selection

People confuse these.

### Feature engineering

Create **new features**

Example

```
shock_index
BMI
pulse_pressure
```

---

### Feature selection

Choose **which features to keep**

Example

```
491 variables
↓
LASSO
↓
25 predictors
```

---

# 6. Why Feature Engineering Matters Even More in Healthcare

Clinical datasets often have:

- missing values
    
- messy coding
    
- weird distributions
    
- domain-specific relationships
    

So models rely heavily on **human insight**.

Good features = better medicine.

---

# 7. The Modern ML Trend

Historically:

```
ML success = feature engineering skill
```

Now deep learning learns features automatically.

But in **tabular data** (like yours):

Feature engineering still dominates.

Most Kaggle competitions are won by **feature engineering**, not fancy models.

---

# 8. The Feature Engineering Mindset

Ask these questions:

1️⃣ Does this variable capture a **real-world mechanism**?

Example:

```
shock_index → shock physiology
```

2️⃣ Is the relationship **nonlinear**?

Example:

```
age^2
log(income)
```

3️⃣ Do variables **interact**?

Example:

```
age × smoking
```

4️⃣ Does missingness **mean something**?

---

# 9. A Good Learning Resource

Best practical guide:

**Feature Engineering for Machine Learning**

Andrew Ng (Coursera ML Specialization)

Also excellent:

Kaggle feature engineering guide  
[https://www.kaggle.com/learn/feature-engineering](https://www.kaggle.com/learn/feature-engineering)

---

# 10. One Important Reality

In real ML work:

```
Data cleaning
Feature engineering
80% of the work
```

Model training is only **20%**.

---

