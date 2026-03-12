---
share: true
---
2026-03-12  12:39
Tags:


---

# 1️⃣ Start: the regression objective

Your model wants to minimize:
$$
[  
RSS = \sum (y_i - X_i\beta)^2  
]
$$
---

# 2️⃣ Add regularization = add a boundary
![[Pasted image 20260312123944.png|Pasted image 20260312123944.png]]

Regularization says:

> You cannot choose any β you want.  
> β must stay inside a constraint region.

That region is the **green shape** in the slides.

Your optimization becomes:

```
Find the lowest RSS ellipse
that still touches the allowed region
```

The **touching point = final coefficients**.

This is the **key idea of regularization geometry**.

---

# 3️⃣ Ridge regression (circle)

Slide:
$$
[  
\beta_1^2 + \beta_2^2 \le s  
]
$$
This forms a **circle**.

Why?

Because

```
x² + y² = radius²
```

is a circle.

So Ridge constraint looks like:
![[Pasted image 20260312124009.png|Pasted image 20260312124009.png]]
Your RSS ellipse expands until it **touches the circle**.

Important observation:

👉 Circles have **no corners**.

So the touching point usually looks like:

```
β1 ≠ 0
β2 ≠ 0
```

That’s why **Ridge rarely produces zero coefficients**.

It just **shrinks them smaller**.

---

# 4️⃣ LASSO (diamond)

Constraint:
$$
[  
|\beta_1| + |\beta_2| \le s  
]
$$
This produces a **diamond shape**.

Why?

Because:

```
|x| + |y| = constant
```

forms a diamond.
![[Pasted image 20260312124022.png|Pasted image 20260312124022.png]]

Now something important happens.

The **diamond has sharp corners**.

Those corners lie exactly on the axes:

```
β1 = 0
or
β2 = 0
```

When the ellipse expands, it is **very likely to hit a corner first**.

Example:

```
touches here
      ▲
     /X\
```

That means:

```
β1 = 0
β2 ≠ 0
```

or

```
β2 = 0
β1 ≠ 0
```

This is **feature selection**.

That is why:

> **LASSO sets coefficients exactly to zero.**

---

# 5️⃣ The famous comparison picture

Your last slide shows this:
![[Pasted image 20260312124100.png|Pasted image 20260312124100.png]]

Left = LASSO  
Right = Ridge

```
LASSO

   ◇
ellipse hits corner
→ coefficient = 0


RIDGE

   ○
ellipse hits smooth edge
→ both coefficients non-zero
```

This geometric property explains **everything** about L1 vs L2.

---

# 6️⃣ Now Elastic Net

Elastic Net combines both penalties.

The formula on your slide:
$$
[  
RSS + \lambda \left(\frac{1-\alpha}{2} \sum \beta_j^2 + \alpha \sum |\beta_j|\right)  
]
$$
Meaning:

```
penalty = mix of L1 + L2
```

Where:

```
α = 1 → pure LASSO
α = 0 → pure Ridge
0 < α < 1 → Elastic Net
```

So Elastic Net region looks like:

```
between circle and diamond
```

That’s exactly what your last picture shows.

```
diamond shape
rounded by ridge
```

![[Pasted image 20260312124125.png|Pasted image 20260312124125.png]]

---

# 7️⃣ Why Elastic Net exists

LASSO has a weakness.

If predictors are **highly correlated**, LASSO tends to:

```
pick one variable
drop the others
```

Example:

```
blood_pressure
pulse_pressure
shock_index
```

They are correlated.

LASSO may choose only **one**.

But medically maybe you want **all related signals**.

Elastic Net fixes this.

It:

```
shrinks like Ridge
selects like LASSO
```

So correlated variables can stay together.

---

# 8️⃣ Quick intuition summary

|Method|Shape|Effect|
|---|---|---|
|Ridge|circle|shrink coefficients|
|LASSO|diamond|feature selection|
|Elastic Net|rounded diamond|shrink + select|

---

# 9️⃣ One thing that helps ML understanding a lot

Most ML optimization problems are actually:

```
loss surface (ellipses)
+
constraint region
=
intersection point
```

This geometric view shows up everywhere:

- LASSO
    
- SVM
    
- logistic regression
    
- deep learning optimization
    

---
