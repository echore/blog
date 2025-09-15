---
share: true
---
2025-09-15  09:36
Tags: [[Bordeaux|Bordeaux]]
#### what is statistic inference?
Statistical inference is the process of using sample data to make educated conclusions about a larger population, while carefully accounting for uncertainty.


![[Pasted image 20250915093547.png|Pasted image 20250915093547.png]]``
# General formulation of the likelihood

## 1. Statistical model
We have data:
$$
Y_1, Y_2, \ldots, Y_n \ \text{iid with density function } f_Y^\theta(\cdot)
$$

The **statistical model** assumes each observation comes from the same distribution depending on an unknown parameter \(\theta\).

---

## 2. Likelihood
The likelihood function is:
$$
\mathcal{L}(\theta; Y) = f_Y^\theta(Y) = \prod_{i=1}^n f_{Y_i}^\theta(Y_i)
$$

- Here the data \(Y_i\) are considered fixed once observed.  
- The likelihood is a **function of the parameter \(\theta\)**.

---

## 3. Maximum Likelihood Estimator (MLE)
The **MLE** is the value of \(\theta\) that maximizes the likelihood:
$$
\hat{\theta} = \arg\max_\theta \ \mathcal{L}(\theta; Y)
$$

Equivalently:
$$
\sup_{\theta \in \Theta} \ \mathcal{L}(\theta; Y) = \mathcal{L}(\hat{\theta}; Y)
$$

---

## 4. Example: Bernoulli/Binomial case
Suppose we observed \(7\) successes and \(3\) failures.  
The likelihood function is:
$$
\mathcal{L}(\pi) = \pi^7 (1-\pi)^3
$$

---

## 5. Log-likelihood
It is easier to maximize the log of the likelihood:
$$
\ell(\pi) = \log \mathcal{L}(\pi) = 7 \log(\pi) + 3 \log(1-\pi)
$$

---

## 6. Derivation of the MLE
Differentiate the log-likelihood and set derivative to zero:
$$
\frac{\partial \ell(\pi)}{\partial \pi} 
= \frac{7}{\pi} - \frac{3}{1-\pi} = 0
$$

Solve for \(\pi\):
$$
\frac{7}{\pi} = \frac{3}{1-\pi}
\quad \Longrightarrow \quad
7(1-\pi) = 3\pi
\quad \Longrightarrow \quad
\pi = \frac{7}{10} = 0.7
$$

Thus, the MLE is:
$$
\hat{\pi} = 0.7
$$

---

## ✅ Key takeaways
- Likelihood = function of parameters given data.  
- MLE = parameter value that maximizes likelihood.  
- Log-likelihood simplifies products into sums.  
- For Bernoulli/binomial models, the MLE is the sample proportion.


