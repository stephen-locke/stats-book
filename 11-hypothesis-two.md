# Hypothesis Testing — Two Samples {#hypothesis-two}

## Comparing Two Groups

The one-sample tests in Chapter 10 compared a single group to a known benchmark or historical standard. In practice, many of the most important business questions involve comparing **two groups**:

- Does Store A have a higher average transaction value than Store B?
- Do employees perform better before or after a training program?
- Do male and female customers spend different amounts, on average?
- Does the new marketing campaign produce a higher response rate than the old one?

This chapter develops statistical tests for comparing two populations. We cover two fundamental designs: **independent samples** (two separate, unrelated groups) and **paired samples** (the same subjects measured twice, or naturally matched pairs).

## Independent vs. Paired Samples

The first decision in a two-sample analysis is determining whether the samples are independent or paired.

**Independent samples** come from two separate groups with no natural connection between the observations in one group and those in the other. Each sample is drawn independently.

Examples:
- Sales data from Store A vs. Store B (different customers, different locations)
- Test scores of employees who received training vs. those who did not
- Customer satisfaction ratings from two different product lines

**Paired samples** (also called **dependent samples** or **matched pairs**) occur when there is a natural, one-to-one pairing between observations in the two groups.

Examples:
- Before-and-after measurements on the **same individuals** (e.g., employee productivity before and after training)
- Measurements on **matched pairs** of subjects (e.g., two branches matched by store size; one implements a policy, the other doesn't)
- Two measurements on the same item (e.g., left and right machine calibration readings)

<div class="callout note-box">
<span class="callout-title">Note</span>
Identifying whether samples are paired or independent is crucial. Using the wrong procedure produces incorrect results. Ask: "Is there a natural, one-to-one relationship between an observation in Group 1 and a specific observation in Group 2?" If yes, use a paired test. If no, use an independent-samples test.
</div>

## Two-Sample t-Test for Independent Means

We want to test $H_0: \mu_1 = \mu_2$ (the two population means are equal) against one of:
- $H_a: \mu_1 \neq \mu_2$ (two-tailed)
- $H_a: \mu_1 > \mu_2$ (right-tailed)
- $H_a: \mu_1 < \mu_2$ (left-tailed)

### Case 1: Equal Variances (Pooled t-Test)

If we have reason to believe the two populations have the same (or similar) variance, we can pool the two sample variances into a single estimate, giving a more precise test.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Pooled variance:**
$$s_p^2 = \frac{(n_1-1)s_1^2 + (n_2-1)s_2^2}{n_1+n_2-2}$$

**Pooled t-test statistic:**
$$t = \frac{(\bar{x}_1 - \bar{x}_2) - (\mu_1 - \mu_2)_0}{s_p\sqrt{1/n_1 + 1/n_2}}$$

Under $H_0: \mu_1 = \mu_2$, the $(\mu_1 - \mu_2)_0$ term equals 0.

**Degrees of freedom:** $df = n_1 + n_2 - 2$
</div>

### Case 2: Unequal Variances (Welch's t-Test)

When the population variances are not equal (or we are unsure), we use **Welch's t-test**, which does not assume equal variances. This is the more conservative and generally safer approach when in doubt.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Welch's t-test statistic:**
$$t = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{s_1^2/n_1 + s_2^2/n_2}}$$

**Degrees of freedom (Welch's approximation — Excel computes this automatically):**
$$df \approx \frac{(s_1^2/n_1 + s_2^2/n_2)^2}{\frac{(s_1^2/n_1)^2}{n_1-1} + \frac{(s_2^2/n_2)^2}{n_2-1}}$$

Round down to the nearest whole number. This df is typically not a whole number, which is why we let Excel calculate it.
</div>

In practice, **use Welch's test (unequal variances) by default** unless you have a specific reason to assume equal variances. It is more robust and Excel's ToolPak implements it directly.

<div class="callout example-box">
<span class="callout-title">Example</span>
**Comparing Sales at Two Locations**

A retail manager wants to know whether average daily sales differ between Downtown (Location 1) and Suburban (Location 2) stores. She samples sales for 15 randomly selected days at each location.

- Location 1 (Downtown): $n_1 = 15$, $\bar{x}_1 = \$12,450$, $s_1 = \$1,820$
- Location 2 (Suburban): $n_2 = 15$, $\bar{x}_2 = \$10,890$, $s_2 = \$2,340$

$H_0: \mu_1 = \mu_2$; $H_a: \mu_1 \neq \mu_2$; $\alpha = 0.05$

Using Welch's test:
$$t = \frac{12,450 - 10,890}{\sqrt{1,820^2/15 + 2,340^2/15}} = \frac{1,560}{\sqrt{220,907 + 365,160}} = \frac{1,560}{\sqrt{586,067}} = \frac{1,560}{765.5} = 2.038$$

Excel calculates $df \approx 25.9$ (round to 25) and gives p-value = `=T.DIST.2T(2.038, 25)` ≈ 0.052.

Since p-value (0.052) > $\alpha$ (0.05), **fail to reject $H_0$**.

**Conclusion:** At the 5% significance level, there is insufficient evidence to conclude that mean daily sales differ between the two locations. The result is close to the significance threshold — the manager might consider a larger sample.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Two-Sample t-Test Using the Data Analysis ToolPak:**

1. Go to **Data → Data Analysis**.
2. Choose one of:
   - **t-Test: Two-Sample Assuming Equal Variances** (pooled t-test)
   - **t-Test: Two-Sample Assuming Unequal Variances** (Welch's t-test — recommended by default)
3. Set **Variable 1 Range** and **Variable 2 Range** to your two data columns.
4. Set **Hypothesized Mean Difference** to 0 (for $H_0: \mu_1 = \mu_2$).
5. Check **Labels** if your ranges include headers.
6. Set **Alpha** (the significance level, e.g., 0.05).
7. Specify an **Output Range** and click **OK**.

Excel produces: mean, variance, observations, df, t stat, P(T<=t) one-tail, t critical one-tail, P(T<=t) two-tail, t critical two-tail.

**Reading the output:**
- Use "P(T<=t) two-tail" and "t Critical two-tail" for a two-tailed test.
- Use "P(T<=t) one-tail" and "t Critical one-tail" for a one-tailed test (and check that the sign of $t$ is consistent with your $H_a$).
</div>

## The Paired t-Test

For paired data, we compute the **difference** $d_i = x_{1i} - x_{2i}$ for each pair, then perform a one-sample t-test on those differences.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
Let $d_i = x_{1i} - x_{2i}$ be the difference for each pair, $\bar{d}$ the mean of all differences, and $s_d$ the standard deviation of the differences.

**Paired t-test statistic:**
$$t = \frac{\bar{d} - \mu_{d_0}}{s_d / \sqrt{n}}$$

where $n$ is the number of pairs and $\mu_{d_0} = 0$ under $H_0: \mu_1 = \mu_2$ (equivalently, $\mu_d = 0$).

**Degrees of freedom:** $df = n - 1$
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Before-and-After Training Program**

An HR department implements a new sales training program for 8 representatives and measures their weekly sales (in units) before and after.

| Rep | Before ($x_1$) | After ($x_2$) | Difference $d = x_2 - x_1$ |
|-----|--------------|--------------|--------------------------|
| 1 | 42 | 50 | +8 |
| 2 | 55 | 58 | +3 |
| 3 | 38 | 44 | +6 |
| 4 | 61 | 65 | +4 |
| 5 | 47 | 51 | +4 |
| 6 | 52 | 49 | -3 |
| 7 | 44 | 52 | +8 |
| 8 | 58 | 63 | +5 |

$\bar{d} = (8+3+6+4+4-3+8+5)/8 = 35/8 = 4.375$

$s_d = \sqrt{\frac{\sum(d_i - \bar{d})^2}{n-1}}$ (compute in Excel using `=STDEV.S()` on the difference column) = $\approx 3.54$

$H_0: \mu_d = 0$; $H_a: \mu_d > 0$ (we expect sales to increase); $\alpha = 0.05$; $df = 7$

$$t = \frac{4.375 - 0}{3.54/\sqrt{8}} = \frac{4.375}{1.251} = 3.497$$

p-value = `=T.DIST.RT(3.497, 7)` ≈ 0.0049

Since p-value (0.005) < $\alpha$ (0.05), **reject $H_0$**.

**Conclusion:** The training program produced a statistically significant increase in weekly sales. The mean improvement of approximately 4.4 units per week is statistically significant at the 1% level.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Paired t-Test Using the Data Analysis ToolPak:**

1. Enter "Before" values in one column and "After" values in an adjacent column.
2. Go to **Data → Data Analysis → t-Test: Paired Two Sample for Means → OK**.
3. Set **Variable 1 Range** to the "Before" column and **Variable 2 Range** to the "After" column.
4. **Hypothesized Mean Difference** = 0.
5. Click **OK**.

The output is identical in format to the independent samples t-test. Select one-tail or two-tail p-value based on your $H_a$.

**Alternatively**, compute differences in a new column using a formula (e.g., `=B2-A2`), then run a one-sample t-test on the differences using the formulas from Chapter 10.
</div>

## Two-Sample Z-Test for Proportions

When both samples are large, we can compare two population proportions.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$H_0: p_1 = p_2$ (equivalently, $p_1 - p_2 = 0$)

**Pooled proportion:** $\hat{p} = \frac{x_1 + x_2}{n_1 + n_2}$ (combines successes from both samples)

**Z-test statistic:**
$$Z = \frac{\hat{p}_1 - \hat{p}_2}{\sqrt{\hat{p}(1-\hat{p})\left(\frac{1}{n_1} + \frac{1}{n_2}\right)}}$$

**Conditions:** $n_1\hat{p} \geq 5$, $n_1(1-\hat{p}) \geq 5$, $n_2\hat{p} \geq 5$, $n_2(1-\hat{p}) \geq 5$
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Comparing Email Campaign Response Rates**

A marketing team sends two versions of an email campaign. Campaign A goes to 500 customers; 85 respond (respond rate $\hat{p}_1 = 85/500 = 0.17$). Campaign B goes to 500 different customers; 110 respond ($\hat{p}_2 = 110/500 = 0.22$). At $\alpha = 0.05$, does Campaign B have a significantly higher response rate?

$H_0: p_1 = p_2$; $H_a: p_1 < p_2$ (left-tailed: we expect Campaign B is better)

Pooled proportion: $\hat{p} = (85+110)/(500+500) = 195/1000 = 0.195$

$$Z = \frac{0.17 - 0.22}{\sqrt{0.195(0.805)(1/500 + 1/500)}} = \frac{-0.05}{\sqrt{0.195 \times 0.805 \times 0.004}} = \frac{-0.05}{\sqrt{0.000628}} = \frac{-0.05}{0.02506} = -1.995$$

p-value = $P(Z < -1.995)$ = `=NORM.S.DIST(-1.995, TRUE)` ≈ 0.0230

Since p-value (0.023) < $\alpha$ (0.05), **reject $H_0$**.

**Conclusion:** Campaign B has a statistically significantly higher response rate than Campaign A at the 5% level. The marketing team should proceed with Campaign B.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Two-Proportion Z-Test in Excel:**

Excel does not have a built-in two-proportion test, but it is straightforward to compute in cells. Here is a template:

```
n1 = 500,  x1 = 85,  phat1 = x1/n1
n2 = 500,  x2 = 110, phat2 = x2/n2
phat_pooled = (x1+x2)/(n1+n2)
SE = SQRT(phat_pooled*(1-phat_pooled)*(1/n1+1/n2))
Z = (phat1-phat2)/SE
p_value_left  = NORM.S.DIST(Z, TRUE)
p_value_right = 1-NORM.S.DIST(Z, TRUE)
p_value_two   = 2*NORM.S.DIST(-ABS(Z), TRUE)
```
</div>

## Effect Size: Cohen's d

Statistical significance tells us whether an effect is real (not due to chance). It does not tell us whether the effect is **practically important**. A sample of 10,000 might detect a difference of \$0.05 in mean transaction value as statistically significant — but is a 5-cent difference worth acting on?

**Effect size** measures the magnitude of the difference, independent of sample size.

**Cohen's d** for two-sample comparisons measures how many standard deviations apart the two means are:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$d = \frac{|\bar{x}_1 - \bar{x}_2|}{s_p}$$

where $s_p$ is the pooled standard deviation.

**Guidelines (Cohen's conventions):**
- $d \approx 0.2$: small effect
- $d \approx 0.5$: medium effect
- $d \approx 0.8$: large effect
</div>

<div class="callout note-box">
<span class="callout-title">Note</span>
Always consider both statistical significance AND practical significance (effect size) when interpreting results. A large sample can make tiny, trivial differences statistically significant. A small sample might miss a meaningful difference. Ask: "Even if this difference is real, is it large enough to matter for our decision?"
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Independent Samples</dt>
<dd>Two samples where the observations in one group have no natural pairing with those in the other; the groups are separate and unrelated.</dd>

<dt>Paired Samples (Dependent Samples)</dt>
<dd>Two samples where each observation in one group is naturally paired with exactly one observation in the other group (e.g., before/after measurements on the same subject).</dd>

<dt>Pooled Variance ($s_p^2$)</dt>
<dd>A weighted average of the two sample variances, used in the equal-variance t-test when the populations are assumed to have the same variance.</dd>

<dt>Welch's t-Test</dt>
<dd>A two-sample t-test that does not assume equal population variances; generally preferred over the pooled t-test when variance equality is uncertain.</dd>

<dt>Paired t-Test</dt>
<dd>A one-sample t-test applied to the differences $d_i = x_{1i} - x_{2i}$ from paired observations; tests whether the mean difference differs from zero.</dd>

<dt>Effect Size</dt>
<dd>A standardized measure of the magnitude of a difference or relationship, independent of sample size; tells you whether an effect is practically meaningful.</dd>

<dt>Cohen's d</dt>
<dd>An effect size measure for comparing two means; the difference in means divided by the pooled standard deviation.</dd>

<dt>Practical Significance</dt>
<dd>Whether a statistically significant effect is large enough to matter in a real-world business context. Distinct from statistical significance.</dd>
</dl>
</div>

---

## Exercises {-}

1. Classify each study design as **independent samples** or **paired samples** and explain your reasoning:
   a. Fifteen employees are given a skills test before a training program and again after; their two scores are compared.
   b. A company surveys 200 male customers and 200 female customers separately and compares their average spending.
   c. A researcher pairs each store in the treatment group with a "similar" store in the control group (matched by size and location) and compares their sales growth.
   d. A random sample of 50 workers from Shift A and 50 different workers from Shift B complete productivity assessments.

2. Two customer service teams handle the same types of inquiries. Team Alpha ($n_1 = 20$, $\bar{x}_1 = 8.2$ minutes, $s_1 = 2.1$ minutes) and Team Beta ($n_2 = 25$, $\bar{x}_2 = 9.5$ minutes, $s_2 = 2.8$ minutes) are compared on mean call handle time. At $\alpha = 0.05$, is there a significant difference in mean handle time?
   a. State $H_0$ and $H_a$.
   b. Use the **Data Analysis ToolPak** (t-Test: Two-Sample Assuming Unequal Variances) to conduct the test. Report the t statistic, df, and p-value.
   c. State your conclusion.
   d. Compute Cohen's d. How would you characterize the practical significance of the difference?

3. A regional bakery chain tests two pricing strategies. In Region 1 ($n_1 = 30$ stores), a "value" pricing approach yields mean weekly revenue of $\bar{x}_1 = \$8,420$, $s_1 = \$1,150$. In Region 2 ($n_2 = 30$ stores), a "premium" pricing approach yields $\bar{x}_2 = \$9,180$, $s_2 = \$980$. At $\alpha = 0.01$, test whether premium pricing produces significantly higher revenue.

4. An HR department assesses employee productivity (items processed per hour) before and after a new ergonomic workstation program for 10 randomly selected employees:

   | Employee | Before | After |
   |----------|--------|-------|
   | 1 | 34 | 38 |
   | 2 | 28 | 31 |
   | 3 | 42 | 45 |
   | 4 | 37 | 40 |
   | 5 | 31 | 35 |
   | 6 | 45 | 44 |
   | 7 | 29 | 33 |
   | 8 | 38 | 41 |
   | 9 | 40 | 45 |
   | 10 | 33 | 36 |

   a. Why is this a paired test rather than an independent samples test?
   b. Compute the differences ($d_i$ = After − Before) for each employee.
   c. Find $\bar{d}$ and $s_d$.
   d. Use the **Data Analysis ToolPak (Paired t-Test)** or compute the t statistic directly. At $\alpha = 0.05$, did productivity improve significantly?

5. An online retailer runs an A/B test of two checkout page designs. Design A was shown to 800 customers; 152 completed a purchase. Design B was shown to 800 different customers; 184 completed a purchase. At $\alpha = 0.05$, does Design B have a significantly higher conversion rate?
   a. Compute $\hat{p}_1$, $\hat{p}_2$, and $\hat{p}_{pooled}$.
   b. Compute the Z-test statistic.
   c. Find the p-value and state your conclusion.

6. *Two coffee shop locations are compared on customer spending. Location North: $n_1 = 45$, $\bar{x}_1 = \$6.80$, $s_1 = \$1.90$. Location South: $n_2 = 38$, $\bar{x}_2 = \$7.30$, $s_2 = \$2.40$. Test at $\alpha = 0.05$ whether Location South customers spend significantly more on average. Then compute Cohen's d and discuss whether the difference is practically meaningful for the business.*
