## **📌 Probability Basics**

---

### **1. Conditional Probability**
**What it is:**
The probability of an event happening **given that another event has already happened**.
*Example:* Probability of rain **given** that the sky is cloudy.

**Why it exists:**
Helps us update our beliefs based on new information.
*Problem solved:* Without it, we couldn’t make predictions based on related events (e.g., medical tests, weather forecasts).

**Tradeoffs:**
- Requires knowing the probability of the "given" event.
- Can get complex with many dependent events.

---

### **2. Bayes’ Theorem**
**What it is:**
A formula to **update the probability of a hypothesis** based on new evidence.
*Example:* If a disease test is 99% accurate, and 1% of people have the disease, what’s the probability you have the disease **if you test positive**?

**Why it exists:**
Allows us to reverse conditional probabilities (from "probability of evidence given hypothesis" to "probability of hypothesis given evidence").
*Problem solved:* Helps in medical diagnosis, spam filtering, and machine learning.

**Tradeoffs:**
- Needs a **prior probability** (initial guess), which can be hard to estimate.
- Can be **computationally heavy** for complex problems.

---

### **3. Likelihood vs. Probability**
| Term | What it means | Example |
|------|--------------|---------|
| **Probability** | How likely an **outcome** is, given fixed parameters. | Probability of rolling a 6 on a die. |
| **Likelihood** | How likely **parameters** are, given observed data. | How likely a die is fair if you roll three 6s in a row. |

**Why it exists:**
- **Probability** helps predict outcomes.
- **Likelihood** helps estimate unknowns (e.g., "Is this coin fair?").
*Problem solved:* Separates prediction from parameter estimation.

**Tradeoffs:**
- Likelihood isn’t a probability (doesn’t sum to 1), which can be confusing.

---

---

## **📊 Statistical Estimation**

---

### **4. Maximum Likelihood Estimation (MLE)**
**What it is:**
Finds the **most likely parameters** that explain the observed data.
*Example:* If you flip a coin 10 times and get 7 heads, MLE estimates the probability of heads as **70%**.

**Why it exists:**
Provides a **systematic way** to guess parameters (e.g., mean, variance) from data.
*Problem solved:* Without MLE, we’d have no objective way to estimate parameters.

**Tradeoffs:**
- **Overfits** with small datasets (assumes data is perfect).
- Doesn’t use **prior knowledge** (unlike MAP).

---

### **5. MAP Estimation (Maximum A Posteriori)**
**What it is:**
Like MLE, but **includes prior knowledge** (e.g., "I think this coin is fair").
*Example:* If you believe a coin is fair (prior), but see 7 heads in 10 flips, MAP balances both to estimate the probability.

**Why it exists:**
Combines **data + prior beliefs** for better estimates.
*Problem solved:* Useful when data is limited (e.g., rare diseases).

**Tradeoffs:**
- **Depends on the prior**—if the prior is wrong, estimates can be biased.
- More complex than MLE.

---

---

## **📈 Distributions & Relationships**

---

### **6. Gaussian (Normal) Distribution**
**What it is:**
A **bell-shaped curve** where most data clusters around the mean.
*Example:* Heights of people, IQ scores, measurement errors.

**Why it exists:**
Many natural phenomena follow this pattern.
*Problem solved:* Simplifies modeling of continuous data.

**Tradeoffs:**
- Assumes **symmetry** (not all real-world data is symmetric).
- **Outliers** can distort results.

---

### **7. Covariance Matrices**
**What it is:**
A table showing **how much two variables change together**.
*Example:* A matrix showing how stock prices of Apple and Google move together.

**Why it exists:**
Helps understand **relationships between multiple variables** at once.
*Problem solved:* Used in finance, machine learning (e.g., PCA).

**Tradeoffs:**
- Hard to interpret for large datasets.
- Doesn’t show **causation**, only correlation.

---
### **8. Correlation vs. Covariance**
| Term | What it means | Example | Range |
|------|--------------|---------|-------|
| **Covariance** | Raw measure of how two variables change together. | If temperature ↑ and ice cream sales ↑, covariance is positive. | (-∞, +∞) |
| **Correlation** | **Standardized** covariance (always between -1 and 1). | Temperature and ice cream sales have a correlation of **+0.9**. | [-1, 1] |

**Why it exists:**
- **Covariance** tells direction and magnitude.
- **Correlation** makes it **comparable** across different scales.
*Problem solved:* Helps compare relationships fairly.

**Tradeoffs:**
- Correlation **ignores magnitude** (only direction and strength).
- Neither implies **causation**.

---

---

## **⚖️ Model Evaluation & Tradeoffs**

---

### **9. Bias-Variance Tradeoff**
**What it is:**
The **balance** between:
- **Bias** (error due to oversimplifying the problem).
- **Variance** (error due to overfitting to noise in data).

*Example:*
- **High bias:** A straight line trying to fit a curvy dataset (underfitting).
- **High variance:** A line that twists to pass through every single point (overfitting).

**Why it exists:**
All models have **some error**—this tradeoff helps minimize it.
*Problem solved:* Guides model selection (e.g., choosing polynomial degree).

**Tradeoffs:**
- **Reducing bias** (e.g., more complex model) → **Increases variance**.
- **Reducing variance** (e.g., more data) → **May not reduce bias**.

---

### **10. Entropy & Cross-Entropy**
| Term | What it means | Example |
|------|--------------|---------|
| **Entropy** | Measures **uncertainty/randomness** in data. | High entropy: Fair coin (50-50). Low entropy: Loaded coin (90-10). |
| **Cross-Entropy** | Measures how well a **model’s predictions** match the **true data**. | If your model predicts 80% rain but it doesn’t rain, cross-entropy penalizes this. |

**Why it exists:**
- **Entropy:** Helps in data compression, decision trees.
- **Cross-Entropy:** Used in **classification tasks** (e.g., logistic regression).
*Problem solved:* Quantifies information and prediction error.

**Tradeoffs:**
- Cross-entropy **penalizes wrong predictions heavily** (good for learning but can be sensitive).

---

### **11. KL Divergence**
**What it is:**
Measures how **different** one probability distribution is from another.
*Example:* Comparing a model’s predicted distribution to the true distribution.

**Why it exists:**
Helps in **model comparison**, information theory, and reinforcement learning.
*Problem solved:* Tells us how much **information is lost** when approximating one distribution with another.

**Tradeoffs:**
- **Not symmetric** (KL(P||Q) ≠ KL(Q||P)).
- Can be **infinite** if one distribution assigns 0 probability to an event that the other doesn’t.

---

### **12. Expectation & Variance**
| Term | What it means | Example |
|------|--------------|---------|
| **Expectation (Mean)** | The **average** value you’d expect. | Expected roll of a die: 3.5. |
| **Variance** | How **spread out** the data is. | Low variance: Most rolls are close to 3.5. High variance: Rolls are all over the place. |

**Why it exists:**
- **Expectation:** Summarizes the **center** of data.
- **Variance:** Summarizes the **spread** of data.
*Problem solved:* Helps describe and compare datasets.

**Tradeoffs:**
- Variance is **sensitive to outliers** (use **standard deviation** for interpretability).

---

---
## **🔍 Hypothesis Testing & Metrics**

---

### **13. Hypothesis Testing Basics**
**What it is:**
A statistical method to **make decisions** using data.
*Example:* Testing if a new drug works better than a placebo.

**Key Terms:**
- **Null Hypothesis (H₀):** Default assumption (e.g., "Drug has no effect").
- **Alternative Hypothesis (H₁):** What you want to prove (e.g., "Drug works").
- **p-value:** Probability of seeing the data **if H₀ is true**. Low p-value → Reject H₀.

**Why it exists:**
Provides a **framework** to test claims objectively.
*Problem solved:* Helps in A/B testing, medical trials, quality control.

**Tradeoffs:**
- **Type I Error (False Positive):** Rejecting H₀ when it’s true (e.g., saying a drug works when it doesn’t).
- **Type II Error (False Negative):** Failing to reject H₀ when it’s false (e.g., missing a real effect).

---

### **14. Precision / Recall / F1**
| Metric | Formula | What it means | Example |
|--------|---------|--------------|---------|
| **Precision** | TP / (TP + FP) | % of **predicted positives** that are correct. | Out of 100 emails marked as spam, 90 are actually spam. Precision = 90%. |
| **Recall** | TP / (TP + FN) | % of **actual positives** found. | Out of 100 actual spam emails, 80 were caught. Recall = 80%. |
| **F1 Score** | 2 × (Precision × Recall) / (Precision + Recall) | **Balance** between precision and recall. | If Precision=90%, Recall=80%, F1 ≈ 85%. |

**Why it exists:**
- **Precision:** Important when **false positives are costly** (e.g., spam filtering).
- **Recall:** Important when **false negatives are costly** (e.g., cancer detection).
*Problem solved:* Helps evaluate **classification models**.

**Tradeoffs:**
- **Precision vs. Recall:** Increasing one often **decreases the other**.

---

### **15. ROC / AUC**
**What it is:**
- **ROC Curve:** Plots **True Positive Rate (Recall)** vs. **False Positive Rate** at different thresholds.
- **AUC (Area Under Curve):** Single number (0 to 1) summarizing model performance.

*Example:* A curve that’s closer to the top-left corner means a better model.

**Why it exists:**
- **ROC:** Shows tradeoff between **sensitivity (recall)** and **specificity**.
- **AUC:** Measures **overall ability** to distinguish classes.
*Problem solved:* Helps compare models **independent of threshold**.

**Tradeoffs:**
- **AUC can be misleading** for imbalanced datasets (e.g., 99% negative class).

---
### **16. Calibration**
**What it is:**
A model’s **predicted probabilities** should match the **actual probabilities**.
*Example:* If a weather forecast says "70% chance of rain," it should rain **70% of the time** when that prediction is made.

**Why it exists:**
Ensures **predictions are reliable** (not just accurate in classification).
*Problem solved:* Critical for **risk assessment** (e.g., medical diagnosis, loan approvals).

**Tradeoffs:**
- **Calibrated models** may be **less confident** (lower sharpness).
