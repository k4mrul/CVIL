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
The famous "bell curve." Many things in nature cluster around an average, with fewer and fewer occurrences as you move away from it.
*Example:* Human heights, measurement errors, test scores. Most people are near the average; extreme giants or dwarfs are rare.

**Why it exists:**
Many natural phenomena follow this pattern.
*Problem solved:* Simplifies modeling of continuous data.

**Tradeoffs:**
Not everything is Gaussian. Income, earthquake sizes, and social media followers follow "heavy-tailed" distributions. Force-fitting a bell curve to these leads to massive underestimation of extreme events.

---

### **7. Covariance Matrices**
**What it is:**
A table showing **how much two/multiple variables change together**.
*Example:*
- Temperature and ice cream sales have positive covariance (when one goes up, the other goes up).
- Temperature and coat sales have negative covariance.
A matrix just stores these relationships for many variables at once.

**Why it exists:**
In machine learning, features often move together. Knowing this helps models understand the data's structure.
*Problem solved:* Used in finance, machine learning (e.g., PCA).

**Tradeoffs:**
Covariance is sensitive to the scale of variables. If you measure height in millimeters instead of meters, covariance explodes even though the relationship hasn't changed.

---
### **8. Correlation vs. Covariance**
| Term | What it means | Example | Range |
|------|--------------|---------|-------|
| **Covariance** | Raw measure of how two variables change together. | If temperature ↑ and ice cream sales ↑, covariance is positive. | (-∞, +∞) |
| **Correlation** | **Standardized** covariance (always between -1 and 1). | Temperature and ice cream sales have a correlation of **+0.9**. | [-1, 1] |

**Why it exists:**
- **Covariance** tells direction and magnitude. Raw number. Hard to interpret whether 500 is "strong" or "weak" because it depends on units.
- **Correlation** makes it **comparable** across different scales. Scaled to always be between -1 and +1. +1 means perfectly in sync, -1 means perfectly opposite, 0 means no linear relationship.

*Example:*
Covariance between height and weight might be 150 (kg·cm). Correlation might be 0.85. The 0.85 immediately tells you "strong relationship" without knowing the units.

*Problem solved:* Helps compare relationships fairly. We need a standardized way to compare relationships across different datasets.

**Tradeoffs:**
Correlation only captures linear relationships. Two variables can be perfectly related in a curved way and still have 0 correlation.

---

---

## **⚖️ Model Evaluation & Tradeoffs**

---

### **9. Bias-Variance Tradeoff**
**What it is:**
The **balance** between:
- **Bias** Your model is too simple and consistently misses patterns (underfitting).
- **Variance** Your model is too complex and memorizes noise (overfitting).

*Example:*
- **High bias:** A straight line trying to fit a curvy dataset (underfitting).
- **High variance:** Fitting a squiggly line that passes through every data point. You fail on new data.

**Why it exists:**
You can't minimize both at the same time. Simpler models generalize better but miss details; complex models capture details but overfit.

*Problem solved:* Guides model selection (e.g., choosing polynomial degree).

**Tradeoffs:**
- **Reducing bias** (e.g., more complex model) → **Increases variance**.
- **Reducing variance** (e.g., more data) → **May not reduce bias**.
- Finding the sweet spot requires judgment, more data, or regularization. There is no free lunch.

---

### **10. Entropy & Cross-Entropy**
| Term | What it means | Example |
|------|--------------|---------|
| **Entropy** | Measures **uncertainty/randomness** in data. | High entropy: Fair coin (50-50). Low entropy: Loaded coin (90-10). |
| **Cross-Entropy** | Measures how well a **model’s predictions** match the **true data**. | If your model predicts 80% rain but it doesn’t rain, cross-entropy penalizes this. |

**Example:**
Example: You predict a coin is 90% heads, but it's actually fair. Cross-entropy measures how wrong your predictions feel. Lower cross-entropy = better predictions.

**Why it exists:**
- **Entropy:** Helps in data compression, decision trees.
- **Cross-Entropy:** Used in **classification tasks** (e.g., logistic regression).
  
*Problem solved:* Quantifies information and prediction error.

**Tradeoffs:**
- Cross-Entropy heavily punishes confident wrong answers. If you predict 99% "cat" and it's a dog, the penalty is enormous. This can make training unstable with noisy labels.

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
Provides a **framework** to test claims objectively. Humans are terrible at intuitively judging randomness. We see patterns in noise. Hypothesis testing imposes discipline.
*Problem solved:* Helps in A/B testing, medical trials, quality control.

**Tradeoffs:**
- **Type I Error (False Positive):** Rejecting H₀ when it’s true (e.g., saying a drug works when it doesn’t).
- **Type II Error (False Negative):** Failing to reject H₀ when it’s false (e.g., missing a real effect).

---

### **14. Precision / Recall / F1**
| Metric | Formula | What it means | Example |
|--------|---------|--------------|---------|
| **Precision** | TP / (TP + FP) | % of **predicted positives** that are correct. | Out of 100 emails marked as spam, how many were actually spam. If 90 percent is actually spam, Precision = 90%. |
| **Recall** | TP / (TP + FN) | % of **actual positives** found. | Out of 100 actual spam emails, how many did you catch. If 80 were caught. Recall = 80%. |
| **F1 Score** | 2 × (Precision × Recall) / (Precision + Recall) | **Balance** between precision and recall. | If Precision=90%, Recall=80%, F1 ≈ 85%. |

**Why it exists:**
- **Precision:** Important when **false positives are costly** (e.g., spam filtering).
- **Recall:** Important when **false negatives are costly** (e.g., cancer detection).
*Problem solved:* Helps evaluate **classification models**.

*Example*: Cancer screening:
- High recall, low precision: You flag almost everyone (catch all cancers, but many healthy people get scared).
- High precision, low recall: You only flag obvious cases (few false alarms, but miss some cancers).

**Tradeoffs:**
- **Precision vs. Recall:** Precision and recall usually pull in opposite directions. Improving one often hurts the other. F1 forces you to confront this balance.


---

### **15. ROC / AUC**
**What it is:**
- **ROC Curve:** A graph showing the tradeoff between true positive rate (recall) and false positive rate as you change your model's decision threshold.
- **AUC (Area Under Curve):** Single number (0 to 1) summarizing model performance.

*Example:* A curve that’s closer to the top-left corner means a better model.
A spam filter can be strict or lenient. ROC shows what happens across all possible strictness levels. AUC = 0.85 means if you pick a random spam email and a random real email, there's an 85% chance the model ranks the spam as "more spammy."

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
