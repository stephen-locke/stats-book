# Confidence Intervals {#confidence-intervals}

## Estimation and Uncertainty

When a polling firm surveys 1,000 voters and reports that "48% support Candidate A, with a margin of error of ±3 percentage points," they are communicating a **confidence interval**. When a company reports that "average customer wait time is 4.2 minutes, plus or minus 0.4 minutes," that's a confidence interval too.

Confidence intervals are the primary tool of **estimation** — the first major branch of inferential statistics. Rather than pretending we know the population parameter exactly, a confidence interval honestly acknowledges the uncertainty in our estimate by providing a **range of plausible values** for the parameter.

In this chapter, we develop confidence intervals for population means (with known and unknown population standard deviations) and for population proportions. We also clarify a common misconception about what a confidence interval actually means.

## The Concept of a Confidence Interval

A **confidence interval (CI)** is an interval of values, computed from sample data, that is likely to contain the true population parameter.

The structure of every confidence interval is:
$$\text{Point Estimate} \pm \text{Margin of Error}$$

The **point estimate** is the sample statistic (e.g., $\bar{x}$ or $\hat{p}$). The **margin of error (ME)** reflects how much the estimate might vary from sample to sample — it is determined by the confidence level and the standard error.

### What Does "95% Confidence" Mean?

This is the most commonly misunderstood concept in introductory statistics.

A **95% confidence interval** means: if we repeated the sampling process many times and constructed a 95% confidence interval each time, **approximately 95% of those intervals would contain the true population parameter**.

<div class="callout warning-box">
<span class="callout-title">Caution</span>
A 95% confidence interval does **NOT** mean:
- "There is a 95% probability that the population parameter falls in this interval." (The parameter is fixed; it either is or is not in the interval.)
- "95% of the data values fall in this interval." (The CI is about the parameter, not individual data points.)
- "If we collected new data, 95% of new observations would fall in this interval." (That would be a prediction interval, not a confidence interval.)

The correct interpretation: "We used a method that produces intervals containing the true parameter 95% of the time. This particular interval is one of those intervals."
</div>

### The Confidence Level and Critical Values

The **confidence level** is typically expressed as a percentage: 90%, 95%, or 99% are most common. Higher confidence requires a wider interval (greater margin of error).

The **critical value** ($z^*$ or $t^*$) is the value from a standard distribution that corresponds to the chosen confidence level. For the Z-interval:

| Confidence Level | $z^*$ |
|-----------------|-------|
| 90% | 1.645 |
| 95% | 1.960 |
| 99% | 2.576 |

These values come from the fact that for a 95% CI, we want the middle 95% of the standard normal distribution, which leaves 2.5% in each tail: `=NORM.S.INV(0.975)` = 1.960.

## Confidence Interval for a Population Mean (σ Known)

When the population standard deviation $\sigma$ is known (rare in practice, but useful as a starting point), we use the **Z-interval**.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Confidence interval for $\mu$ when $\sigma$ is known:**
$$\bar{x} \pm z^* \cdot \frac{\sigma}{\sqrt{n}}$$

The margin of error is:
$$ME = z^* \cdot \frac{\sigma}{\sqrt{n}} = z^* \cdot \sigma_{\bar{x}}$$

**Conditions:** The sample is a simple random sample AND (population is normal OR $n \geq 30$).
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Estimating Mean Customer Spending**

A retail chain knows from long historical records that the population standard deviation of customer transaction values is $\sigma = \$22$. A new store opens, and a random sample of $n = 50$ transactions is observed. The sample mean is $\bar{x} = \$67.40$. Construct a 95% confidence interval for the true mean transaction value at the new store.

$z^* = 1.960$ (for 95% confidence)

$ME = 1.960 \times \frac{22}{\sqrt{50}} = 1.960 \times 3.111 = 6.10$

95% CI: $67.40 \pm 6.10 = (\$61.30, \ \$73.50)$

**Interpretation:** We are 95% confident that the true mean customer transaction at the new store is between \$61.30 and \$73.50.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Computing the Margin of Error for Z-interval in Excel:**

`=CONFIDENCE.NORM(alpha, sigma, n)`
- `alpha` = 1 − confidence level (for 95% CI, alpha = 0.05)
- `sigma` = population standard deviation
- `n` = sample size

This returns the margin of error. Add and subtract it from the sample mean.

**Example:** For the retail scenario above:
- Cell B1: sample mean = 67.40
- `=CONFIDENCE.NORM(0.05, 22, 50)` → 6.10 (margin of error)
- Lower bound: `=B1 - CONFIDENCE.NORM(0.05, 22, 50)` → 61.30
- Upper bound: `=B1 + CONFIDENCE.NORM(0.05, 22, 50)` → 73.50
</div>

## The t-Distribution and Confidence Interval for a Population Mean (σ Unknown)

In practice, $\sigma$ is almost never known. We must estimate it using the sample standard deviation $s$. When we do this, the resulting test statistic no longer follows a standard normal distribution — it follows a **t-distribution**.

### Properties of the t-Distribution

The **t-distribution** is a family of bell-shaped, symmetric distributions (one for each value of **degrees of freedom**). Key properties:

- Symmetric and bell-shaped like the normal, but with **heavier tails** — more probability in the extremes.
- Defined by one parameter: **degrees of freedom (df) = $n - 1$**.
- As df increases (larger $n$), the t-distribution approaches the standard normal distribution.
- For $n \geq 30$, the t-distribution is nearly identical to the normal distribution.

The heavy tails of the t-distribution reflect our additional uncertainty when we estimate $\sigma$ from the sample. This uncertainty is greatest for small samples.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Confidence interval for $\mu$ when $\sigma$ is unknown (t-interval):**
$$\bar{x} \pm t^*_{n-1} \cdot \frac{s}{\sqrt{n}}$$

where:
- $s$ = sample standard deviation
- $n$ = sample size
- $t^*_{n-1}$ = critical value from the t-distribution with $n-1$ degrees of freedom and the desired confidence level

**Conditions:** Simple random sample AND (population is approximately normal OR $n \geq 30$).
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Finding t Critical Values and Computing t-intervals in Excel:**

`=T.INV.2T(alpha, df)` — Two-tailed t critical value
- `alpha` = 1 − confidence level (for 95% CI, alpha = 0.05)
- `df` = degrees of freedom = $n - 1$

**Example:** For 95% CI with $n = 25$: `=T.INV.2T(0.05, 24)` → 2.064

`=CONFIDENCE.T(alpha, std_dev, n)` — Margin of error for t-interval
- `alpha` = 1 − confidence level
- `std_dev` = sample standard deviation $s$
- `n` = sample size

**Example:** 95% CI with $s = 15$, $n = 25$:
`=CONFIDENCE.T(0.05, 15, 25)` → margin of error ≈ 6.20
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Estimating Mean Processing Time**

An operations manager samples $n = 20$ customer orders and measures the processing time (in minutes) for each. Results: $\bar{x} = 14.7$ minutes, $s = 3.2$ minutes. Construct a 90% confidence interval for the mean processing time for all orders.

**Check conditions:** We assume the processing times are approximately normally distributed (reasonable for this type of data).

$df = 20 - 1 = 19$

$t^*_{19}$ for 90% CI: `=T.INV.2T(0.10, 19)` → 1.729

$ME = 1.729 \times \frac{3.2}{\sqrt{20}} = 1.729 \times 0.7155 = 1.237$ minutes

90% CI: $14.7 \pm 1.2 = (13.5, \ 15.9)$ minutes

**Interpretation:** We are 90% confident that the true mean processing time is between 13.5 and 15.9 minutes.
</div>

## Confidence Interval for a Population Proportion

When the variable of interest is a proportion rather than a mean, we use the following interval.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Confidence interval for a population proportion $p$:**
$$\hat{p} \pm z^* \cdot \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$$

where $\hat{p}$ = sample proportion, $n$ = sample size, and $z^*$ is the critical Z-value for the desired confidence level.

**Conditions:**
- Simple random sample
- $n\hat{p} \geq 5$ and $n(1-\hat{p}) \geq 5$ (at least 5 "successes" and 5 "failures" in the sample)
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Customer Satisfaction Survey**

A company surveys $n = 400$ customers; 284 report being "satisfied" or "very satisfied." Construct a 95% confidence interval for the true proportion of all customers who are satisfied.

$\hat{p} = 284/400 = 0.71$

Check conditions: $400(0.71) = 284 \geq 5$ ✓, $400(0.29) = 116 \geq 5$ ✓

$ME = 1.960 \times \sqrt{\frac{0.71 \times 0.29}{400}} = 1.960 \times \sqrt{0.0005148} = 1.960 \times 0.02269 = 0.0445$

95% CI: $0.71 \pm 0.0445 = (0.6655, \ 0.7545)$, or approximately **(66.6%, 75.5%)**

**Interpretation:** We are 95% confident that the true proportion of satisfied customers is between 66.6% and 75.5%.
</div>

## Choosing Sample Size

Before collecting data, we can determine the sample size needed to achieve a desired margin of error.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Sample size for estimating a mean** (with desired ME and known $\sigma$):
$$n = \left(\frac{z^* \cdot \sigma}{ME}\right)^2$$
Always round UP to the next whole number.

**Sample size for estimating a proportion** (with desired ME):
$$n = \frac{(z^*)^2 \cdot \hat{p}(1-\hat{p})}{ME^2}$$

If $\hat{p}$ is unknown, use $\hat{p} = 0.5$ (which gives the largest — most conservative — required sample size).
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Planning a Market Research Survey**

A marketing team wants to estimate the proportion of customers interested in a new product. They want the margin of error to be no more than ±3% at 95% confidence. They have no prior estimate of the proportion.

Using $\hat{p} = 0.5$ (most conservative):
$$n = \frac{(1.960)^2 \times 0.5 \times 0.5}{(0.03)^2} = \frac{3.8416 \times 0.25}{0.0009} = \frac{0.9604}{0.0009} \approx 1,068$$

They need a minimum sample of **1,068 customers**.

If their preliminary research suggests $\hat{p} \approx 0.30$:
$$n = \frac{(1.960)^2 \times 0.30 \times 0.70}{(0.03)^2} = \frac{3.8416 \times 0.21}{0.0009} = \frac{0.8067}{0.0009} \approx 897$$

Using the prior estimate reduces the required sample to **897 customers**.
</div>

## Interpreting Confidence Intervals in Business Reports

When you encounter confidence intervals in business contexts, keep these points in mind:

**Wider intervals reflect more uncertainty.** A 99% CI is always wider than a 95% CI for the same data. A sample of $n=30$ produces wider intervals than $n=300$.

**Confidence level is not quality.** A 99% CI is not "better" than a 95% CI — it's just more conservative. The appropriate confidence level depends on the consequences of being wrong.

**Overlapping intervals suggest no significant difference.** If the 95% CIs for two groups overlap substantially, the groups may not truly differ. (A more rigorous comparison requires a hypothesis test — Chapter 10.)

**Report all three components:** point estimate, interval bounds (or margin of error), and confidence level. An interval without a confidence level is meaningless.

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Full Confidence Interval Calculation Workflow in Excel:**

Set up a small calculation table:

| Cell | Label | Formula / Value |
|------|-------|----------------|
| B1 | Sample mean | `=AVERAGE(data range)` |
| B2 | Sample std dev | `=STDEV.S(data range)` |
| B3 | Sample size | `=COUNT(data range)` |
| B4 | Confidence level | 0.95 |
| B5 | Alpha | `=1-B4` |
| B6 | Margin of error | `=CONFIDENCE.T(B5,B2,B3)` |
| B7 | Lower bound | `=B1-B6` |
| B8 | Upper bound | `=B1+B6` |

This template is reusable for any data set — just change the data range reference.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Confidence Interval (CI)</dt>
<dd>An interval of values, computed from sample data, that is estimated to contain the true population parameter with a specified level of confidence.</dd>

<dt>Point Estimate</dt>
<dd>A single numerical value used to estimate a population parameter (e.g., $\bar{x}$ estimates $\mu$, $\hat{p}$ estimates $p$).</dd>

<dt>Margin of Error (ME)</dt>
<dd>The half-width of a confidence interval; $ME = \text{critical value} \times \text{standard error}$.</dd>

<dt>Confidence Level</dt>
<dd>The probability (expressed as a percentage) that the method used to construct the confidence interval will produce an interval containing the true parameter; commonly 90%, 95%, or 99%.</dd>

<dt>Critical Value ($z^*$ or $t^*$)</dt>
<dd>The value from a standard distribution separating the middle (confidence) area from the tails; depends on the confidence level and the distribution used.</dd>

<dt>t-Distribution</dt>
<dd>A family of symmetric, bell-shaped distributions with heavier tails than the normal; used when $\sigma$ is unknown and estimated by $s$. Defined by degrees of freedom.</dd>

<dt>Degrees of Freedom (df)</dt>
<dd>A parameter of the t-distribution; for a single-sample t-interval, df = $n - 1$. More degrees of freedom → t-distribution closer to normal.</dd>

<dt>Standard Error of the Mean</dt>
<dd>The estimated standard deviation of the sampling distribution of $\bar{x}$: $s/\sqrt{n}$ when $\sigma$ is unknown.</dd>
</dl>
</div>

---

## Exercises {-}

1. A financial analyst collects a random sample of $n = 40$ quarterly earnings reports from small-cap technology companies. The sample mean earnings growth rate is $\bar{x} = 8.4\%$ with sample standard deviation $s = 3.1\%$.
   a. Construct a **95% confidence interval** for the mean earnings growth rate.
   b. Construct a **99% confidence interval** for the same data.
   c. Which interval is wider? Explain why in plain language.
   d. What would happen to the width of the interval if the sample size were increased to $n = 160$?

2. A human resources manager at a manufacturing firm wants to estimate the mean number of sick days taken per employee per year. A random sample of $n = 25$ employees is selected; the data shows $\bar{x} = 4.8$ days and $s = 2.1$ days. Assume sick days are approximately normally distributed.
   a. What are the appropriate degrees of freedom?
   b. Find the critical $t$ value for a 90% confidence interval.
   c. Compute the 90% confidence interval.
   d. Interpret the interval in the context of the problem.

3. A market research survey asks 500 randomly selected consumers whether they plan to purchase a new product in the next 90 days. 185 say yes.
   a. Calculate the sample proportion $\hat{p}$.
   b. Check the conditions for the proportion confidence interval.
   c. Construct a **95% confidence interval** for the true proportion of consumers who plan to purchase.
   d. Construct a **90% confidence interval** and compare its width to the 95% CI.

4. A new coffee blend is tested by 35 randomly selected tasters. Each taster rates the blend on a scale from 1 to 10. Results: $\bar{x} = 7.4$, $s = 1.6$.
   a. Construct a 95% confidence interval.
   b. The blend's developer claims the true mean rating is at least 8.0. Is this claim plausible based on the CI? Explain.

5. A hotel chain wants to estimate the average rating it receives on a popular travel review site, accurate to within ±0.1 stars at 95% confidence. Preliminary data suggests $\sigma \approx 0.8$ stars.
   a. How large a sample of reviews should the hotel analyze?
   b. If the chain reduces the desired margin of error to ±0.05 stars, how does the required sample size change?

6. A telecommunications company surveys customers after service calls to estimate the proportion who are "very satisfied." They want the margin of error to be no more than ±4% at 99% confidence.
   a. Using no prior estimate, what sample size is required?
   b. If a pilot study finds $\hat{p} = 0.68$, what sample size is required?

7. A company claims its customer service calls average 4.5 minutes or less. A random sample of $n = 36$ calls yields $\bar{x} = 5.1$ minutes with $s = 1.8$ minutes.
   a. Construct a 95% CI for the mean call time.
   b. Does the 95% CI support or cast doubt on the company's claim? Explain.

8. *An investor is comparing the mean monthly returns of two portfolio strategies. Strategy A: $n_A = 24$ months, $\bar{x}_A = 1.8\%$, $s_A = 0.9\%$. Strategy B: $n_B = 24$ months, $\bar{x}_B = 2.3\%$, $s_B = 1.4\%$. Construct separate 95% CIs for the mean monthly return of each strategy. Do the intervals overlap? What does the overlap (or lack thereof) suggest about whether the two strategies have different true mean returns? (Note: a formal two-sample test is covered in Chapter 11.)*
