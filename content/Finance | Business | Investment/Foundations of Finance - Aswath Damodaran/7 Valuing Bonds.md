---
share: true
date: 2025-05-07
---
![[session7.pdf|session7.pdf]]


## 💵 What is a Bond?

A **bond** is a type of loan — you lend money to a government or company, and they promise:

1. To pay you **interest every year** (called **coupon payments**)
2. To return your **principal** at the end (called **face value** or **par value**)

---

## 📘 Bond Details (Example)

- **Coupon rate**: 3%  
  → You receive **\$30 per year** (3% of \$1000 face value)  
- **Maturity**: 10 years  
- **Face value**: \$1000  
- **Market risk-free interest rate**: 2%  

---

## 📉 Why Do We Discount?

Because **\$1 in the future is worth less than \$1 today**, we **discount** all future payments to their present value using the **risk-free rate (2%)**.

---

## 🧮 Step-by-Step Valuation

### 🟩 Step 1: Present Value of Coupons (Annuity)

You receive \$30 every year for 10 years.

Annuity formula:

$$
PV_{\text{coupons}} = C \cdot \left( \frac{1 - (1 + r)^{-n}}{r} \right)
$$

Plug in values:

$$
PV_{\text{coupons}} = 30 \cdot \left( \frac{1 - (1 + 0.02)^{-10}}{0.02} \right) = 30 \cdot 8.9826 \approx 269.48
$$

---

### 🟦 Step 2: Present Value of Face Value (Lump Sum)

You get \$1000 at the end of 10 years.

$$
PV_{\text{face}} = \frac{1000}{(1 + 0.02)^{10}} \approx \frac{1000}{1.219} \approx 820.35
$$

---

### 📊 Final Bond Price

Add both components:

$$
\text{Bond Price} = 269.48 + 820.35 = \boxed{1089.83}
$$

---

## 🔺 Why is it Trading Above Par?

Because the **coupon rate (3%) is higher** than the **market interest rate (2%)**, investors are willing to **pay more** than \$1000 to earn that higher income.

This is called a **premium bond**.

---

## 🔑 Key Takeaways

- Discount **coupons as an annuity**
- Discount **face value as a lump sum**
- Use the **market rate (not the coupon rate)** for discounting
- If **coupon rate > market rate**, bond price **> par**
- If **coupon rate < market rate**, bond price **< par**

---


## 📉 Default Risk and the Default Spread

### 🛑 What is Default (Credit) Risk?

When a bond is issued by a company or government **with risk**, there's a chance you **won’t get your full coupon or principal payments**.

This is called:

> **Default Risk** or **Credit Risk**

---

### ⚠️ Why It Matters

To compensate for this risk, investors (you) demand a **higher interest rate** than the risk-free rate.

The extra interest is called the:

> **Default Spread**

---

### 💰 Adjusted Discount Rate

When valuing a risky bond:

$$
\text{Discount Rate} = \text{Risk-Free Rate} + \text{Default Spread}
$$

This **increases the discount rate**, which **reduces the bond price**, reflecting its higher risk.

---

### 📘 Example:

- Risk-Free Rate: 3%
- Default Spread: 2%

$$
\text{Adjusted Rate} = 3\% + 2\% = \boxed{5\%}
$$

Now use **5%** to discount the bond’s cash flows, not 3%.

This gives a **lower valuation** for the same promised payments.

### 🧠 Key Idea

> The more likely the issuer might default, the higher the return you should demand — and the lower the bond’s fair value today.

---


### Investment Grade vs. High Yield

- **Investment Grade Bonds** = BBB (S&P/Fitch) or Baa3 (Moody’s) and above
    
    - These are considered **low default risk**
        
- **Below Investment Grade Bonds** = BB and below
    
    - Also called **"junk bonds"** or **"high-yield bonds"**
        
    - Higher yields because they’re **riskier**

---

#### What is a Floating Rate Bond?

- A **floating rate bond** pays interest that **adjusts regularly** (e.g., every 3 or 6 months).
    
- The interest payment is tied to a **reference rate** like LIBOR, SOFR, or a government bond yield, **plus a fixed spread**.
#### Why Should It Trade at Par?

- Because the coupon **resets to match the market**, you’re always getting a **fair current return**.
    
- There's **no gain or loss** from changes in market interest rates — unlike fixed-rate bonds.

![[session7test.pdf|session7test.pdf]]

![[session7soln.pdf|session7soln.pdf]]

When a bond’s **market price = face value (par)**, then:   **YTM = coupon rate**

## Takeaway:
- All else equal, it’s safer to buy **low default risk bonds** and consider **floating rate bonds** to reduce interest rate risk and preserve capital stability. ?
- The longer the maturity of the bond and the lower the coupon rate, the more sensitive the value will be to changes in interest rates.
