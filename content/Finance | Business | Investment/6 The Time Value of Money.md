---
share: true
date: 2025-05-06
---
![[session6.pdf|session6.pdf]]

## 💰 Present Value and the Discount Rate

When someone promises to give you money in the future, it's important to ask:
**How much is that money worth today?**

To answer that, we use a concept called **Present Value (PV)**.

---

### 📘 Formula: Present Value

$$
PV = \frac{FV}{(1 + r)^n}
$$

Where:
- \( PV \): Present Value (value today)
- \( FV \): Future Value (amount received in the future)
- \( r \): Discount rate (as a decimal, e.g., 0.05 for 5%)
- \( n \): Number of years into the future

---

### 🧮 Example 1: 5% Discount Rate

Someone promises to give you **$1000** in **5 years**.  
If the discount rate is **5%**, then:

$$
PV = \frac{1000}{(1 + 0.05)^5} = \frac{1000}{1.27628} \approx 784.00
$$

So, **$1000 in 5 years** is worth about **$784 today**.

---

### 🧮 Example 2: 10% Discount Rate

Now suppose the discount rate is **10%** instead:

$$
PV = \frac{1000}{(1 + 0.10)^5} = \frac{1000}{1.61051} \approx 620.92
$$

So, **$1000 in 5 years** is worth only **$620.92 today** at a higher discount rate.

---

### 🧠 Why Does This Matter?

- A **higher discount rate** makes future money **less valuable today**.
- The discount rate reflects:
  - Your **preference for current consumption**
  - **Expected inflation**
  - **Risk or uncertainty** of the cash flow
  - Your **opportunity cost** (what you could earn elsewhere)

---

### 🔁 Bonus: Compounding vs. Discounting

- **Discounting** = converting future money to today’s value
- **Compounding** = growing today’s money to see its future value

They are **opposites** on the same timeline!

---

![[session6test.pdf|session6test.pdf]]

![[session6soln.pdf|session6soln.pdf]]

## 🧾 Valuing Ron Judge's 10-Year Contract

Ron Judge is offered:

- **$8 million per year** for the first **5 years**
- **$12 million per year** for the next **5 years**
- Payments are made at the **end of each year**
- The appropriate **discount rate is 5%**

We break this into two parts:

---

### 🔹 Part 1: PV of \$8M per year for 5 years

This is a standard annuity. Use the **present value of an ordinary annuity** formula:

$$
PV = C \times \left[ \frac{1 - (1 + r)^{-n}}{r} \right]
$$

Where:
- \( C = 8 \) (million)
- \( r = 0.05 \)
- \( n = 5 \)

So:

$$
PV_1 = 8 \times \left[ \frac{1 - (1 + 0.05)^{-5}}{0.05} \right]
= 8 \times \left[ \frac{1 - 0.78353}{0.05} \right]
= 8 \times 3.54595 = 28.37
$$

**→ Present value of years 1–5: \$28.37 million**

---

### 🔹 Part 2: PV of \$12M per year from year 6 to 10

First, compute the PV **as of year 5**:

$$
PV_5 = 12 \times \left[ \frac{1 - (1 + 0.05)^{-5}}{0.05} \right]
= 12 \times 4.32948 = 51.95
$$

Now, discount that back to today (year 0):

$$
PV_2 = \frac{51.95}{(1 + 0.05)^5}
= \frac{51.95}{1.27628} = 40.70
$$

**→ Present value of years 6–10: \$40.70 million**

---

### ✅ Total Present Value

Add both parts:

$$
PV_{\text{total}} = PV_1 + PV_2 = 28.37 + 40.70 = \boxed{69.07 \text{ million}}
$$

---

Great — let’s go one row at a time and I’ll rephrase everything in **very plain English**, with **concrete examples** to help make each point clear.

---

### | **a. It should not be higher than the discount rate**

#### ❌ Why this is **mathematically necessary** but **not economically enough**:

> ✅ Yes, the formula FCFr−g\frac{FCF}{r - g} **only works if** g<rg < r, because otherwise you'd divide by zero or get a negative value.
> 
> ❌ But that doesn’t mean **any number below the discount rate is safe**.

**Example**:

- Discount rate r=8%r = 8\%
    
- You try using g=7.5%g = 7.5\%
    
- Even though it’s < 8%, that’s way too high — if your company grows 7.5% forever, it will eventually become **bigger than the entire economy**.
    

🔑 So: **This rule is necessary, but not sufficient**. It’s a basic math limit, not an economic one.

---

### | **c. It should not be higher than the _real_ growth rate of the economy**

#### ✅ This is true **only if** you're using **real (inflation-adjusted)** cash flows.

> **Real cash flows** = already removed inflation.  
> So your growth rate also needs to be in **real terms**.

**Example**:

- Suppose your model projects "free cash flow in today's dollars," like $10M in constant 2025 purchasing power.
    
- If the **real GDP** grows at 2%, then **your company’s real growth shouldn't exceed 2% forever**.
    

🔑 But: **most DCF models use nominal dollars**, so this doesn’t apply unless you **explicitly model in real terms**.

---

### | **d. It should not be higher than the inflation rate**

#### ❌ Too narrow. Inflation is **only part** of economic growth.

> Inflation just tells you that **prices are going up**, but it says nothing about whether the **economy is producing more**.

**Example**:

- If inflation is 2%, and the economy also grows productivity by 1.5%, the **nominal GDP growth** is about 3.5%.
    
- So **companies can grow more than inflation**, without violating sustainability — just **not more than the whole economy**.
    

🔑 Inflation is a **subset** of nominal growth, not a cap by itself.

---

### | **e. It should not be higher than zero**

#### ❌ Overly pessimistic — this would say “no company can ever grow forever.”

> Some businesses **do grow**, just not faster than the economy.

**Example**:

- A stable company like Coca-Cola might grow at **2% forever**, which is **less than nominal GDP**, but definitely more than zero.
    

🔑 Saying “growth must be ≤ 0” is like saying **no company will ever increase revenue long-term** — which is unrealistic.

---

### ✅ So What’s Left?

Only **b. The nominal growth rate of the economy** makes both **economic and mathematical** sense for most normal (nominal) DCF models.

Would you like a chart or visual to summarize this clearly in one glance?
### ✅ Here's why:

In a **perpetual growth model** (used in terminal value calculations in DCF), the **growth rate (g)** represents the rate at which **free cash flows or earnings will grow forever**.

To make this assumption **reasonable and sustainable**, we cap the perpetual growth rate at the **nominal GDP growth rate** of the overall economy. Why?

- If a company grows **faster than the economy forever**, it will eventually **become bigger than the economy itself**, which is **impossible**.
    
- The **nominal GDP growth rate** includes both **real growth** (productivity, population) and **inflation**, making it the upper bound for **nominal cash flows**.