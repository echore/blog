---
share: true
---
2025-09-15  09:36
Tags: [[Bordeaux|Bordeaux]]
# What is statistic inference?
Statistical inference is the process of using sample data to make educated conclusions about a larger population, while carefully accounting for uncertainty.

---


![[Pasted image 20250916154929.png|Pasted image 20250916154929.png]]

# Likelihood — Beginner-friendly explanation

## Step 1: What are we dealing with?

* You have some **data**:  
  $$
  Y = (Y_1, Y_2, \dots, Y_n)^T
  $$  
  👉 Think of $Y$ as the list of numbers you collected from an experiment or survey.

* You also have some **parameters**:  
  $$
  \theta = (\theta_1, \theta_2, \dots, \theta_p)^T
  $$  
  👉 These are the unknown “settings” or “knobs” of the model that produced the data.  
  Example: in a Normal distribution,  
  $$
  \theta = (\mu, \sigma)
  $$  
  where $\mu$ is the mean and $\sigma$ is the standard deviation.

* The function  
  $$
  f_Y^\theta(y)
  $$  
  is the **joint density** (for continuous data) or probability mass function (for discrete data).  
  👉 It tells you how likely a particular dataset $y$ is, given certain parameter values.

---

## Step 2: The likelihood function

The definition is:  
$$
L(\theta; Y) = P(Y \mid \theta) = f_Y^\theta(Y)
$$  

In words:

* **Likelihood** is the probability of seeing your data $Y$, *if* the model parameters were $\theta$.

Notice the perspective shift:

* Normally in probability, we say “given parameters, what’s the probability of the data?”
* In **likelihood**, we flip it: we already have the data (fixed!), and now we ask: *which parameter values $\theta$ would make this data most probable?*

---

## Step 3: An analogy

Imagine you baked some cookies, and you know the recipe had some amount of sugar ($\theta$), but you forgot how much.

* The **data**: the taste of the cookies you already baked.  
* The **model**: how the amount of sugar affects taste.  
* The **likelihood**: for each possible sugar amount ($\theta$), how probable is it that you would have ended up with cookies that taste exactly like these?

You try different values of $\theta$ (e.g., 50g, 100g, 150g sugar) and see which one makes the actual cookies most “likely.”

---

## Step 4: Why do we care?

Because **Maximum Likelihood Estimation (MLE)** uses this idea:

* Pick the parameter value  
  $$
  \hat{\theta}
  $$  
  that maximizes  
  $$
  L(\theta; Y)
  $$  
* That $\hat{\theta}$ is your “best guess” for the true parameter.

## ✅ Key takeaway

* Probability: parameters are fixed, data is random.  
* Likelihood: data is fixed, parameters are variable.  








---

![[Pasted image 20250916161205.png|Pasted image 20250916161205.png]]

# The Score Function

## 1. Definition
The **score function** (or **vector score**) is the first derivative of the **log-likelihood** with respect to the parameter vector.

If we have parameters:
$$
\theta = (\theta_1, \theta_2, \ldots, \theta_p)^T
$$

and log-likelihood:
$$
\ell(\theta; Y) = \log \mathcal{L}(\theta; Y),
$$

then the **score vector** is:
$$
U(\theta) = U(\theta; Y) = \frac{\partial \ell(\theta; Y)}{\partial \theta}
= 
\begin{pmatrix}
\frac{\partial \ell(\theta; Y)}{\partial \theta_1} \\
\vdots \\
\frac{\partial \ell(\theta; Y)}{\partial \theta_p}
\end{pmatrix}.
$$

---

## 2. Example: Bernoulli/Binomial
Suppose we have data $Y_1, Y_2, \ldots, Y_n$ i.i.d. $\sim \text{Bernoulli}(\pi)$.

The log-likelihood is:
$$
\ell(\pi) = \sum_{i=1}^n \Big[ Y_i \log(\pi) + (1-Y_i) \log(1-\pi) \Big].
$$

The score function is the derivative:
$$
U(\pi; Y) = \frac{\partial \ell(\pi)}{\partial \pi}
= \sum_{i=1}^n \left( \frac{Y_i}{\pi} - \frac{1-Y_i}{1-\pi} \right).
$$

---

## 3. Why is it useful?
- The **MLE** is the parameter value $\hat{\theta}$ that makes the score equal to zero:
  $$
  U(\hat{\theta}) = 0
  $$
- In other words: solving the score equation gives the maximum likelihood estimate.

## ✅ Key takeaway
- The **score** is the slope of the log-likelihood with respect to the parameter(s).  
- Setting $U(\theta) = 0$ finds the parameter values where the likelihood is maximized.  







---
![[Pasted image 20250916162150.png|Pasted image 20250916162150.png]]

# Hessian and Fisher Information Matrix

## 1. Hessian
The **Hessian matrix** is the matrix of second derivatives of the log-likelihood with respect to the parameters:
$$
H(\theta) = \frac{\partial^2 \ell(\theta; Y)}{\partial \theta \, \partial \theta^\top}.
$$  

- If $\theta$ is just one parameter (scalar), this reduces to the second derivative.  
- If $\theta$ is a vector of parameters, $H(\theta)$ is a square matrix.  


👉 In simple words: yes, it literally means "differentiate twice."

- First derivative = slope (how fast the function changes).
- Second derivative = curvature (how the slope itself is changing).

### One parameter (scalar case)
If we only have one parameter $\pi$:  
- First derivative:
$$
\frac{\partial \ell(\pi)}{\partial \pi}
$$  

- Second derivative:
$$
\frac{\partial^2 \ell(\pi)}{\partial \pi^2}
$$  

### Multiple parameters (vector case)
If $\theta = (\mu, \sigma)$, then the Hessian is:
$$
H(\theta) =
\begin{bmatrix}
\frac{\partial^2 \ell}{\partial \mu^2} & \frac{\partial^2 \ell}{\partial \mu \, \partial \sigma} \\
\frac{\partial^2 \ell}{\partial \sigma \, \partial \mu} & \frac{\partial^2 \ell}{\partial \sigma^2}
\end{bmatrix}.
$$  

So the Hessian is just “all the second derivatives of the log-likelihood” organized into a matrix.

---

## 2. Fisher Information
The **Fisher information matrix** is defined as the *negative expected value* of the Hessian:
$$
I(\theta) = - \, E_\theta \!\left[ \frac{\partial^2 \ell(\theta; Y)}{\partial \theta \, \partial \theta^\top} \right].
$$  

Equivalently:
$$
I(\theta) = E_\theta[-H(\theta)].
$$  
---

## 3. Interpretation
- $H(\theta)$ = curvature of the log-likelihood at the data (depends on the sample).  
- $I(\theta)$ = expected curvature under the model (population version).  
- Intuitively:  
  *If the likelihood curve is very "sharp" around its maximum, the Fisher information is high → parameters can be estimated precisely.*  

### Why expectation?
- The Hessian depends on your **sample** (random data).
- Fisher Information asks: *on average, across all possible datasets from the model, how sharp is the log-likelihood curve around the true parameter?*

### Why the minus sign?
- The log-likelihood is usually concave (curves downward), so the second derivative is negative.
- Adding a minus sign makes the Fisher Information **positive**.

### Intuition
- If the log-likelihood is **very peaked** → second derivative is strongly negative → Fisher Information is large → parameters can be estimated precisely.
- If the log-likelihood is **flat** → second derivative is near 0 → Fisher Information is small → estimates are uncertain.

---

## 4. Example: Bernoulli/Binomial
For Bernoulli($\pi$):  

The Hessian is:
$$
H(\pi) = \frac{\partial^2 \ell(\pi; Y)}{\partial \pi^2}
= - \frac{\sum_{i=1}^n Y_i}{\pi^2} - \frac{n - \sum_{i=1}^n Y_i}{(1-\pi)^2}.
$$  

The Fisher information is:
$$
I(\pi) = E_\pi \!\left( - \frac{\partial^2 \ell(\pi; Y)}{\partial \pi^2} \right).
$$  

Taking expectations:
$$
I(\pi) = \frac{n}{\pi(1-\pi)}.
$$  








---
