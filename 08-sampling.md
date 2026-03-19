# Sampling Distributions and the Central Limit Theorem {#sampling}

## From Samples to Inference

Up to this point, we have computed sample statistics like $\bar{x}$ and assumed they are reasonably close to the population parameters $\mu$. But how close? How much do sample means vary from sample to sample, and what determines that variability? These are the questions that sampling distributions answer.

The **Central Limit Theorem**, introduced in this chapter, is one of the most remarkable results in all of mathematics. It explains why so many statistical methods work, and it is the key that makes inference from samples to populations valid — even when we know very little about the shape of the original population distribution.

## Sampling Error

Whenever we estimate a population parameter using a sample statistic, we will almost certainly get a slightly wrong answer — not because of carelessness or mistakes, but simply because we observed only part of the population. This is called **sampling error** (or sampling variability).

**Sampling error** is the difference between a sample statistic and the corresponding population parameter:
$$\text{Sampling error for the mean} = \bar{x} - \mu$$

If we randomly selected a different sample, we would get a different $\bar{x}$ and thus a different sampling error. Sampling error is not a mistake — it is an inevitable consequence of working with samples rather than populations.

Key insight: with a larger sample size $n$, sampling error tends to be smaller on average. A sample of 1,000 customers produces an estimate closer to the true population mean than a sample of 10 customers.

## The Sampling Distribution of the Sample Mean

Imagine the following thought experiment: you take a random sample of size $n$ from a population and compute the sample mean $\bar{x}$. Then you put the sample back, take a new sample of the same size, and compute a new $\bar{x}$. You do this hundreds or thousands of times.

The distribution of all these sample means is called the **sampling distribution of the sample mean**.

The sampling distribution is a probability distribution describing the behavior of the sample mean $\bar{x}$ across all possible random samples of size $n$.

This is a theoretical concept — in practice, we take one sample. But understanding what the sampling distribution would look like tells us how reliable our single sample estimate is likely to be.

<div class="callout note-box">
<span class="callout-title">Note</span>
The sampling distribution is the distribution of a statistic (like $\bar{x}$) computed from many repeated samples. It is fundamentally different from the distribution of the raw data in a single sample. The distinction is crucial: the sample distribution describes individual observations, while the sampling distribution describes statistics computed from samples.
</div>

### Mean and Standard Error of $\bar{x}$

Two critical facts about the sampling distribution of $\bar{x}$:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
If simple random samples of size $n$ are taken from a population with mean $\mu$ and standard deviation $\sigma$:

**Mean of the sampling distribution:**
$$\mu_{\bar{x}} = \mu$$

The average of all possible sample means equals the population mean. Sample means are centered on the true population mean — there is no systematic bias.

**Standard error of the mean:**
$$\sigma_{\bar{x}} = \frac{\sigma}{\sqrt{n}}$$

The standard deviation of the sampling distribution of $\bar{x}$ is called the **standard error (SE)**. It decreases as $n$ increases — larger samples produce less variable (more precise) estimates.
</div>

The standard error is one of the most important concepts in applied statistics. Notice:
- When $n = 1$: $\sigma_{\bar{x}} = \sigma$ (as expected — a sample of one has the same variability as the population).
- When $n = 4$: $\sigma_{\bar{x}} = \sigma/2$ (the spread of sample means is halved).
- When $n = 100$: $\sigma_{\bar{x}} = \sigma/10$ (sample means are much more tightly clustered).

**Quadrupling the sample size cuts the standard error in half.** This is the mathematical reason why larger samples give more reliable estimates — but with diminishing returns.

## The Central Limit Theorem

The Central Limit Theorem (CLT) addresses the *shape* of the sampling distribution.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**The Central Limit Theorem:**

For a random sample of size $n$ drawn from a population with mean $\mu$ and standard deviation $\sigma$:

If the population is **normally distributed**, then $\bar{x}$ is exactly normally distributed for **any** $n$.

If the population is **not normally distributed** (skewed, uniform, etc.), then $\bar{x}$ is **approximately normally distributed** when $n$ is sufficiently large — generally, $n \geq 30$ is considered sufficient for most practical situations.

In both cases:
$$\bar{x} \sim N\left(\mu, \frac{\sigma}{\sqrt{n}}\right)$$
</div>

The CLT is remarkable because it says that regardless of how bizarre or skewed the population distribution is, if we take large enough samples, the sample means will follow an approximately normal distribution. This is why the normal distribution is so central to statistics.

<div class="callout example-box">
<span class="callout-title">Example</span>
**CLT in Practice: Customer Transaction Times**

A bank's ATM transaction times are right-skewed (most transactions are quick, but a few take a very long time), with population mean $\mu = 1.8$ minutes and population standard deviation $\sigma = 1.2$ minutes.

If we record the average transaction time for a random sample of **36 transactions**, what is the probability that the sample mean exceeds 2.1 minutes?

The population is not normal, but since $n = 36 \geq 30$, the CLT guarantees $\bar{x}$ is approximately normal.

$$\mu_{\bar{x}} = 1.8, \qquad \sigma_{\bar{x}} = \frac{1.2}{\sqrt{36}} = \frac{1.2}{6} = 0.20$$

$$Z = \frac{\bar{x} - \mu_{\bar{x}}}{\sigma_{\bar{x}}} = \frac{2.1 - 1.8}{0.20} = \frac{0.30}{0.20} = 1.50$$

$$P(\bar{x} > 2.1) = P(Z > 1.50) = 1 - 0.9332 = 0.0668$$

There is about a **6.7%** chance that a sample of 36 transactions has a mean exceeding 2.1 minutes.
</div>

<div class="callout note-box">
<span class="callout-title">Note</span>
When $n \geq 30$, the CLT generally works well for the types of business data you'll encounter in this course. However, if the population is extremely skewed or contains extreme outliers, larger samples (perhaps $n \geq 50$ or $n \geq 100$) may be needed for the approximation to be accurate. When the population is already normal, the CLT applies exactly for any sample size.
</div>

## Applying the CLT to Business Problems

The key steps for sampling distribution problems:

1. Identify $\mu$, $\sigma$, and $n$.
2. Compute the standard error: $\sigma_{\bar{x}} = \sigma/\sqrt{n}$.
3. Verify that the CLT applies ($n \geq 30$ or population is normal).
4. Compute the Z-score for the sample mean of interest: $Z = (\bar{x} - \mu)/\sigma_{\bar{x}}$.
5. Find the probability using the standard normal (Z-table or Excel).

<div class="callout example-box">
<span class="callout-title">Example</span>
**Supply Chain: Average Delivery Time**

A logistics company's delivery times are approximately normal with $\mu = 3.4$ days and $\sigma = 0.8$ days. A new client contract specifies an average delivery time of no more than 3.6 days for shipments. If a month includes 25 shipments to this client, what is the probability that the sample mean of those 25 shipments exceeds 3.6 days (violating the contract)?

$\sigma_{\bar{x}} = 0.8/\sqrt{25} = 0.8/5 = 0.16$ days

(Since the population is normal, CLT applies for any $n$.)

$Z = (3.6 - 3.4)/0.16 = 0.20/0.16 = 1.25$

$P(\bar{x} > 3.6) = P(Z > 1.25) = 1 - 0.8944 = 0.1056$

There is about a **10.6%** chance of violating the contract in any given month — high enough that the logistics manager should investigate ways to reduce delivery time variability.
</div>

## The Sampling Distribution of the Sample Proportion

Many business questions involve proportions rather than means: What proportion of products are defective? What percentage of customers will respond to a promotion? What share of voters supports a policy?

Let $\hat{p}$ (p-hat) be the sample proportion: $\hat{p} = x/n$, where $x$ is the number of "successes" in a sample of size $n$.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
If the true population proportion is $p$, the sampling distribution of $\hat{p}$ has:

**Mean:** $\mu_{\hat{p}} = p$

**Standard error of the proportion:**
$$\sigma_{\hat{p}} = \sqrt{\frac{p(1-p)}{n}}$$

The sampling distribution of $\hat{p}$ is approximately normal when both $np \geq 5$ and $n(1-p) \geq 5$.

To find probabilities for $\hat{p}$, convert to a Z-score:
$$Z = \frac{\hat{p} - p}{\sqrt{p(1-p)/n}}$$
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Customer Satisfaction Survey**

A national retailer knows from comprehensive past surveys that 72% of its customers are "satisfied" or "very satisfied" (population proportion $p = 0.72$). A regional manager surveys a random sample of 150 customers. What is the probability that 75% or more of the 150 sampled customers are satisfied?

Check conditions: $np = 150(0.72) = 108 \geq 5$ ✓, $n(1-p) = 150(0.28) = 42 \geq 5$ ✓

Standard error: $\sigma_{\hat{p}} = \sqrt{0.72 \times 0.28 / 150} = \sqrt{0.001344} \approx 0.03667$

$Z = (0.75 - 0.72)/0.03667 \approx 0.818$

$P(\hat{p} \geq 0.75) = P(Z \geq 0.818) = 1 - 0.7932 = 0.2068$

There is about a **20.7%** chance that the sample proportion is 75% or higher, even if the true population proportion is 72%.
</div>

## Excel Simulation to Illustrate the CLT

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Simulating the Central Limit Theorem in Excel:**

This simulation will show you visually how the sampling distribution of $\bar{x}$ becomes approximately normal as $n$ increases, even if the underlying population is not normal.

**Step 1: Generate a right-skewed population**
In cells A1:A1000, generate random numbers from a skewed distribution:
`=RAND()^0.3` (this creates a right-skewed distribution of values between 0 and 1).
Press **F9** to recalculate.

**Step 2: Generate sample means**
- In column C, generate sample means of size $n = 5$:
  In C1 enter: `=AVERAGE(OFFSET($A$1,(ROW()-1)*5,0,5,1))`
  Copy this formula down to C200 (giving you 200 sample means).
- Repeat in column D with $n = 30$:
  In D1 enter: `=AVERAGE(OFFSET($A$1,(ROW()-1)*30,0,30,1))`
  Copy down to D33 (approximately 1000/30 ≈ 33 samples).

**Step 3: Create histograms**
Create histograms of: (1) the raw data in column A, (2) the sample means in column C ($n=5$), and (3) the sample means in column D ($n=30$).

**Observe:** The raw data (column A) will be visibly skewed. The means with $n=5$ will look less skewed. The means with $n=30$ will look approximately bell-shaped — the CLT in action!
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Computing Standard Error in Excel:**

If your population standard deviation $\sigma$ is known and your sample size is $n$:
`=sigma/SQRT(n)` gives the standard error.

If you are working with a sample (Chapter 9 and beyond) and need to estimate the standard error:
`=STDEV.S(range)/SQRT(COUNT(range))`

This is the estimated standard error, also called the **standard error of the mean (SEM)**.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Sampling Error</dt>
<dd>The difference between a sample statistic and the corresponding population parameter; an inevitable result of studying a sample instead of the full population.</dd>

<dt>Sampling Distribution</dt>
<dd>The probability distribution of a sample statistic (like $\bar{x}$ or $\hat{p}$) across all possible random samples of size $n$ from a population.</dd>

<dt>Standard Error (SE)</dt>
<dd>The standard deviation of a sampling distribution; measures the typical distance between a sample statistic and the population parameter. For $\bar{x}$: $\sigma_{\bar{x}} = \sigma/\sqrt{n}$.</dd>

<dt>Central Limit Theorem (CLT)</dt>
<dd>The theorem stating that the sampling distribution of $\bar{x}$ approaches a normal distribution as $n$ increases, regardless of the shape of the population distribution — typically for $n \geq 30$.</dd>

<dt>Sample Proportion ($\hat{p}$)</dt>
<dd>The proportion of observations in a sample having a characteristic of interest: $\hat{p} = x/n$.</dd>

<dt>Standard Error of the Proportion</dt>
<dd>The standard deviation of the sampling distribution of $\hat{p}$: $\sigma_{\hat{p}} = \sqrt{p(1-p)/n}$.</dd>
</dl>
</div>

---

## Exercises {-}

1. A population of customer account balances has mean $\mu = \$2,450$ and standard deviation $\sigma = \$620$. A random sample of $n = 64$ accounts is selected.
   a. What are the **mean** and **standard error** of the sampling distribution of $\bar{x}$?
   b. Is the CLT applicable here? Why or why not?
   c. What is the probability that the sample mean exceeds \$2,600?
   d. What is the probability that the sample mean falls between \$2,300 and \$2,550?

2. Daily production output at a factory is normally distributed with $\mu = 450$ units and $\sigma = 38$ units. Quality control samples are taken from $n = 16$ production days.
   a. What is the standard error of the sample mean?
   b. What is the probability that the sample mean daily output is between 440 and 465 units?
   c. Below what sample mean would only 5% of samples fall?

3. A market research firm knows that 45% of adults in a city own a premium streaming service subscription ($p = 0.45$). They survey a random sample of $n = 200$ adults.
   a. Check whether the sampling distribution of $\hat{p}$ can be approximated by a normal distribution.
   b. Find the **mean** and **standard error** of the sampling distribution of $\hat{p}$.
   c. What is the probability that the sample proportion exceeds 0.50?
   d. What is the probability that the sample proportion falls below 0.40?

4. A food packaging company fills boxes to a mean weight of $\mu = 500$ g with $\sigma = 12$ g. An inspector takes a sample of $n = 36$ boxes each day.
   a. What is the probability that the daily sample mean weight falls below 496 g?
   b. If the daily sample mean falls outside of the range $(495, 505)$ g, the production line is adjusted. What is the probability that an adjustment is needed on any given day?
   c. The inspector plans to increase the sample size to $n = 100$. How does this change the probability in part (b)?

5. Explain the Central Limit Theorem in your own words to someone who has never taken a statistics class. Use a specific business example (not the examples from this chapter) to illustrate the concept. Your explanation should not use mathematical notation.

6. *A large credit card company has 500,000 cardholders. The distribution of monthly balances is right-skewed with mean $\mu = \$1,850$ and standard deviation $\sigma = \$960$.*
   a. *Why can't we apply normal probability calculations directly to a single randomly selected cardholder's balance?*
   b. *A sample of $n = 144$ cardholders is randomly selected. What is the probability that the sample mean balance exceeds \$2,000?*
   c. *What sample size would be needed to reduce the standard error below \$50?*
