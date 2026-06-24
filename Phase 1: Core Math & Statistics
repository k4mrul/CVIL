# 1. Conditional Probability

## What it means

Conditional probability means:

> The probability of something happening **given that** something else already happened.

Formula:

```text
P(A | B) = probability of A happening given B happened
```

Example:

Suppose in a class:

* 50 students total
* 20 students play football
* 10 students are girls who play football

Question:

> What is the probability a student is a girl **given that** the student plays football?

```text
P(Girl | Football) = 10 / 20 = 0.5
```

So the answer is **50%**.

## Why it exists

Normal probability asks:

> “How likely is A?”

Conditional probability asks:

> “How likely is A if I already know B?”

This is useful because new information changes probability.

## Problem it solves

It helps us update our thinking when we get extra information.

Example:

* Probability someone has fever may be low.
* But probability someone has fever **given they have flu** is much higher.

## Tradeoff

Conditional probability depends heavily on the information you condition on. Bad or incomplete information can give misleading results.

***

# 2. Bayes’ Theorem

## What it means

Bayes’ theorem helps us reverse conditional probabilities.

Formula:

```text
P(A | B) = P(B | A) × P(A) / P(B)
```

In simple words:

> Bayes’ theorem tells us how to update our belief after seeing evidence.

## Easy example

Imagine a disease test.

* 1% of people have the disease.
* If someone has the disease, the test is positive 99% of the time.
* But the test can also be positive for healthy people.

Bayes’ theorem helps answer:

> If my test is positive, what is the chance I actually have the disease?

This is different from:

> If I have the disease, what is the chance the test is positive?

Many beginners confuse these two.

## Why it exists

Because we often know:

> Probability of evidence given a cause

But we want:

> Probability of cause given evidence

Example:

```text
Known: P(positive test | disease)
Wanted: P(disease | positive test)
```

Bayes’ theorem solves this.

## Problem it solves

It helps with decision-making under uncertainty:

* medical diagnosis
* spam detection
* machine learning
* fraud detection
* weather prediction

## Tradeoff

You need a **prior probability**.

Example:

```text
P(disease)
```

If your prior is wrong, your final answer can also be wrong.

***

# 3. Likelihood vs. Probability

This is very important.

## Probability

Probability asks:

> Given a model, how likely is the data?

Example:

You have a fair coin.

```text
P(heads) = 0.5
```

The model is fixed: fair coin.

## Likelihood

Likelihood asks:

> Given the data, how good is this model?

Example:

You toss a coin 10 times and get 8 heads.

Now you ask:

> Is this coin fair? Or maybe biased?

Likelihood compares different possible models:

```text
Coin has 50% heads?
Coin has 80% heads?
Coin has 90% heads?
```

The model that makes the observed data most likely has the highest likelihood.

## Simple difference

| Concept     | Fixed | Changing |
| ----------- | ----: | -------: |
| Probability | Model |     Data |
| Likelihood  |  Data |    Model |

## Why it exists

In real life, we often have data but do not know the true model.

Example:

* We know customer behavior.
* We want to estimate buying probability.

## Tradeoff

Likelihood is not exactly the same as probability. It does not always sum to 1 across models.

***

# 4. Maximum Likelihood Estimation, MLE

## What it means

MLE means:

> Choose the model parameters that make the observed data most likely.

Example:

You toss a coin 10 times:

```text
Heads = 7
Tails = 3
```

MLE says:

```text
Estimated probability of heads = 7 / 10 = 0.7
```

## Why it exists

We often do not know the true value of something.

Example:

* true coin bias
* average income
* failure rate of a machine
* probability user clicks an ad

MLE gives a systematic way to estimate it from data.

## Problem it solves

It turns observed data into estimated model parameters.

## Tradeoff

MLE can overfit when data is small.

Example:

If you toss a coin once and get heads, MLE says:

```text
P(heads) = 1.0
```

That is too extreme.

***

# 5. MAP Estimation

## What it means

MAP means **Maximum A Posteriori** estimation.

It is like MLE, but it also uses prior belief.

```text
MAP = likelihood + prior belief
```

## Example

You toss a coin once and get heads.

MLE says:

```text
P(heads) = 1.0
```

But MAP may say:

```text
Probably around 0.6, because most coins are not extremely biased.
```

## Why it exists

MLE can become too confident with little data.

MAP fixes this by using prior knowledge.

## Problem it solves

It avoids extreme estimates when data is limited.

## Tradeoff

You must choose a prior.

If the prior is bad, MAP can be biased.

***

# 6. Gaussian Distributions

## What it means

A Gaussian distribution is also called a **normal distribution**.

It has a bell shape.

Example:

* human height
* exam scores
* measurement errors

Most values are near the average, and fewer values are far away.

```text
Mean = center
Variance = spread
```

## Simple example

If average exam score is 70:

* many students score around 70
* fewer score 30 or 100

## Why it exists

Many natural things approximately follow this bell shape.

Also, Gaussian distributions are mathematically convenient.

## Problem it solves

It gives a simple way to model uncertainty.

## Tradeoff

Not all data is Gaussian.

Example:

* income is usually not Gaussian
* house prices are often skewed
* social media followers are not normally distributed

***

# 7. Covariance Matrices

## What it means

A covariance matrix shows how multiple variables change together.

If you have:

* height
* weight
* age

A covariance matrix tells you:

* how height varies
* how weight varies
* how age varies
* how height and weight move together
* how weight and age move together

## Simple idea

If height increases and weight also tends to increase, covariance is positive.

## Why it exists

For multi-variable data, one variance is not enough.

You need to know:

> How variables move together.

## Problem it solves

Useful in:

* machine learning
* statistics
* finance
* PCA
* Gaussian models

## Tradeoff

Covariance depends on units.

Example:

If height is measured in meters vs centimeters, covariance changes.

That makes interpretation harder.

***

# 8. Correlation vs. Covariance

## Covariance

Covariance tells direction:

* positive: variables move together
* negative: one increases, other decreases
* zero: no linear relationship

But covariance depends on scale.

## Correlation

Correlation is a standardized version of covariance.

It is always between:

```text
-1 and +1
```

Example:

```text
+1 = perfect positive relationship
0 = no linear relationship
-1 = perfect negative relationship
```

## Easy example

Height and weight may have positive correlation.

As height increases, weight often increases.

## Why both exist

Covariance is useful mathematically.

Correlation is easier to understand and compare.

## Tradeoff

Correlation only measures **linear** relationship.

Two variables can have a strong curved relationship but low correlation.

***

# 9. Bias-Variance Tradeoff

## What it means

This explains model error.

A model can make mistakes because of:

1. **Bias**
2. **Variance**

## Bias

Bias means the model is too simple.

Example:

Trying to predict house prices using only house size.

It ignores:

* location
* number of rooms
* condition

So it makes simple, repeated mistakes.

## Variance

Variance means the model is too sensitive to training data.

Example:

A model memorizes all training examples.

It performs well on training data but badly on new data.

## Simple analogy

Imagine shooting arrows at a target.

* High bias: arrows are grouped but far from center.
* High variance: arrows are scattered everywhere.
* Good model: arrows are close to center and close to each other.

## Why it exists

It helps explain underfitting and overfitting.

## Problem it solves

It helps us choose model complexity.

## Tradeoff

Usually:

* simpler model → high bias, low variance
* complex model → low bias, high variance

We want a balance.

***

# 10. Entropy

## What it means

Entropy measures uncertainty or disorder.

In machine learning, entropy measures how mixed or unpredictable something is.

## Example

Bag A:

```text
10 red balls, 0 blue balls
```

Very predictable. Entropy is low.

Bag B:

```text
5 red balls, 5 blue balls
```

Harder to predict. Entropy is high.

## Why it exists

It helps measure uncertainty.

## Problem it solves

Used in:

* decision trees
* information theory
* compression
* machine learning loss functions

## Tradeoff

Entropy can be abstract at first. It is not always intuitive without examples.

***

# 11. Cross-Entropy

## What it means

Cross-entropy measures how bad a model’s predicted probabilities are.

## Example

True label:

```text
Cat
```

Model prediction:

```text
Cat: 0.9
Dog: 0.1
```

Good prediction → low cross-entropy.

Another model:

```text
Cat: 0.2
Dog: 0.8
```

Bad prediction → high cross-entropy.

## Why it exists

Accuracy only tells right or wrong.

Cross-entropy also cares about confidence.

## Problem it solves

It trains classification models better.

A model should not only be correct; it should be correctly confident.

## Tradeoff

Cross-entropy punishes confident wrong predictions heavily.

That is usually good, but noisy labels can cause problems.

***

# 12. KL Divergence

## What it means

KL divergence measures how different one probability distribution is from another.

It answers:

> How much information is lost if I use distribution Q instead of true distribution P?

## Example

True weather:

```text
Rain: 50%
Sun: 50%
```

Model prediction:

```text
Rain: 90%
Sun: 10%
```

KL divergence will be large because the model is far from reality.

## Why it exists

It compares probability distributions.

## Problem it solves

Used in:

* machine learning
* Bayesian inference
* variational inference
* language models
* information theory

## Tradeoff

KL divergence is not symmetric.

Usually:

```text
KL(P || Q) ≠ KL(Q || P)
```

So direction matters.

***

# 13. Expectation and Variance

## Expectation

Expectation means the long-term average value.

Example:

Roll a fair die.

Possible values:

```text
1, 2, 3, 4, 5, 6
```

Expected value:

```text
(1+2+3+4+5+6) / 6 = 3.5
```

You can never roll 3.5, but over many rolls, the average approaches 3.5.

## Variance

Variance measures spread.

Example:

Two students have average score 70.

Student A scores:

```text
68, 70, 72
```

Student B scores:

```text
40, 70, 100
```

Both average 70, but Student B has higher variance.

## Why they exist

Expectation tells the center.

Variance tells uncertainty or spread.

## Tradeoff

Mean and variance do not describe everything.

Two datasets can have the same mean and variance but different shapes.

***

# 14. Hypothesis Testing Basics

## What it means

Hypothesis testing helps decide if evidence is strong enough to support a claim.

## Common terms

### Null hypothesis

The default assumption.

Example:

```text
This medicine has no effect.
```

### Alternative hypothesis

What you want to test.

```text
This medicine has an effect.
```

### p-value

The p-value answers:

> If the null hypothesis were true, how surprising is this result?

Small p-value means the result is surprising under the null hypothesis.

## Example

You test a new teaching method.

Null hypothesis:

```text
New method does not improve scores.
```

If students improve a lot, you ask:

> Could this improvement happen by random chance?

## Why it exists

It helps avoid being fooled by random noise.

## Problem it solves

It gives a formal way to test claims using data.

## Tradeoff

A p-value does not prove truth.

Also, statistical significance does not always mean practical importance.

Example:

A medicine may improve recovery by 0.1%. That may be statistically significant but not practically useful.

***

# 15. Precision, Recall, and F1

These are used for classification models.

Example: spam email detection.

## Precision

Precision asks:

> Of all emails predicted as spam, how many were actually spam?

```text
Precision = true spam predictions / all spam predictions
```

High precision means fewer false alarms.

## Recall

Recall asks:

> Of all actual spam emails, how many did we catch?

```text
Recall = caught spam / all actual spam
```

High recall means fewer missed spam emails.

## F1 Score

F1 combines precision and recall.

```text
F1 = balance between precision and recall
```

## Easy example

Cancer detection:

* High recall is important because missing cancer is dangerous.
* High precision is also useful because false alarms cause stress and extra tests.

## Why they exist

Accuracy can be misleading.

Example:

If only 1% of emails are spam, a model that says “not spam” every time gets 99% accuracy but catches no spam.

## Tradeoff

Usually:

* increase precision → recall may decrease
* increase recall → precision may decrease

F1 helps balance them.

***

# 16. ROC and AUC

## ROC

ROC curve shows the tradeoff between:

* True Positive Rate
* False Positive Rate

It tests a model at many decision thresholds.

## Example

A model predicts probability of disease.

Threshold 0.5:

```text
If probability > 0.5, predict disease.
```

Threshold 0.8:

```text
If probability > 0.8, predict disease.
```

Changing the threshold changes false positives and true positives.

## AUC

AUC means **Area Under the Curve**.

It summarizes the ROC curve into one number.

```text
AUC = 1.0 means perfect model
AUC = 0.5 means random guessing
```

## Why it exists

It helps compare classifiers across thresholds.

## Problem it solves

Instead of checking one threshold, ROC/AUC checks many thresholds.

## Tradeoff

AUC can be misleading for imbalanced datasets.

Example:

If fraud cases are very rare, precision-recall curves may be more useful than ROC curves.

***

# 17. Calibration

## What it means

Calibration checks whether predicted probabilities are realistic.

## Example

A weather app says:

```text
Rain chance = 70%
```

If it says this on 100 days, then ideally it should rain on about 70 of those days.

That means the model is well calibrated.

## In machine learning

If a model predicts:

```text
90% chance of fraud
```

Then among many cases with 90% prediction, about 90% should actually be fraud.

## Why it exists

Some models are accurate but overconfident.

Example:

A model may say:

```text
99% sure
```

But it is only correct 80% of the time.

Calibration fixes or measures that.

## Problem it solves

It makes probabilities more trustworthy for decision-making.

## Tradeoff

Improving calibration may sometimes reduce other metrics like accuracy or ranking performance.

***

# Quick Summary Table

| Topic                   | Simple Meaning                              | Main Use                   |
| ----------------------- | ------------------------------------------- | -------------------------- |
| Conditional probability | Probability after knowing extra information | Updating probability       |
| Bayes’ theorem          | Reverse conditional probability             | Diagnosis, spam, ML        |
| Likelihood              | How well model explains data                | Model fitting              |
| MLE                     | Pick parameter that best explains data      | Estimation                 |
| MAP                     | MLE plus prior belief                       | Estimation with prior      |
| Gaussian                | Bell-shaped distribution                    | Modeling natural data      |
| Covariance matrix       | Variables moving together                   | Multivariable data         |
| Correlation             | Standardized relationship                   | Easy comparison            |
| Bias-variance           | Simple vs too complex model                 | Avoid under/overfitting    |
| Entropy                 | Uncertainty                                 | Information measure        |
| Cross-entropy           | Prediction probability error                | Classification loss        |
| KL divergence           | Difference between distributions            | Compare probability models |
| Expectation             | Long-term average                           | Center of data             |
| Variance                | Spread of data                              | Uncertainty                |
| Hypothesis testing      | Test claims using data                      | Scientific decisions       |
| Precision               | How many predicted positives are correct    | Avoid false alarms         |
| Recall                  | How many actual positives are found         | Avoid missing cases        |
| F1                      | Balance precision and recall                | Imbalanced classification  |
| ROC/AUC                 | Classifier quality across thresholds        | Model comparison           |
| Calibration             | Are probabilities trustworthy?              | Reliable decisions         |

***

# One Big Example Connecting Many Ideas

Imagine you build a model to detect spam emails.

* **Conditional probability**: probability email is spam given it contains “free money”.
* **Bayes’ theorem**: update spam probability after seeing words.
* **Likelihood**: how well your spam model explains observed emails.
* **MLE**: estimate word probabilities from data.
* **MAP**: estimate word probabilities using data plus prior belief.
* **Precision**: of emails marked spam, how many truly are spam?
* **Recall**: of all spam emails, how many did you catch?
* **F1**: balance precision and recall.
* **ROC/AUC**: evaluate model at many thresholds.
* **Calibration**: if model says 80% spam, is it really spam about 80% of the time?
* **Cross-entropy**: train model to give good probabilities.
* **KL divergence**: compare predicted distribution to true distribution.
* **Bias-variance**: avoid model being too simple or memorizing training emails.

***

If you remember only one idea:

> Statistics and machine learning are mostly about making decisions under uncertainty using data.  
> These concepts help us measure uncertainty, update beliefs, fit models, and evaluate predictions.
