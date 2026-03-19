# Hypothesis Testing — One Sample {#hypothesis-one}

## The Logic of Hypothesis Testing

In Chapter 9, we answered the question: "Based on sample data, what is a plausible range for the population parameter?" Hypothesis testing asks a subtly different question: "Is this specific claim about the population parameter consistent with the evidence in my sample data?"

Hypothesis testing is the workhorse of inferential statistics. Every day, managers and analysts ask questions like: "Has our delivery time improved since the process change?" "Is this store's defect rate higher than the company standard?" "Do customers respond to the new price point at a higher rate than before?" These are all hypothesis tests.

Hypothesis testing is used in:
- **Quality control:** Is the defect rate within specification?
- **Marketing:** Is the new website version converting at a higher rate?
- **Finance:** Has the portfolio return changed significantly?
- **HR:** Has average employee satisfaction improved after a new program?
- **Operations:** Has mean delivery time decreased after a logistics upgrade?

## The Logic and Structure of Hypothesis Testing

### Step 1: State the Hypotheses

Every hypothesis test involves two competing claims about a population parameter:

**The null hypothesis ($H_0$)** is the default, "no change," or "status quo" claim. It is always stated as an equality (or includes equality). It is what we assume to be true unless we have strong evidence otherwise. Think of it as the hypothesis we are trying to disprove.

**The alternative hypothesis ($H_a$ or $H_1$)** is the research claim — what the analyst suspects might actually be true. It represents the conclusion we would draw if we find strong enough evidence against $H_0$.

<div class="callout note-box">
<span class="callout-title">Note</span>
The null hypothesis always contains an equals sign: $H_0: \mu = k$, $H_0: \mu \leq k$, or $H_0: \mu \geq k$. The alternative hypothesis never contains an equals sign: $H_a: \mu \neq k$, $H_a: \mu > k$, or $H_a: \mu < k$.
</div>

### One-Tailed vs. Two-Tailed Tests

The alternative hypothesis determines whether the test is one-tailed or two-tailed.

**Two-tailed test:** The alternative claims the parameter is *different from* a value (either higher or lower). Use when there is no prior directional hypothesis.

$$H_0: \mu = \mu_0 \qquad H_a: \mu \neq \mu_0$$

**Right-tailed test:** The alternative claims the parameter is *greater than* a value.

$$H_0: \mu \leq \mu_0 \qquad H_a: \mu > \mu_0$$

**Left-tailed test:** The alternative claims the parameter is *less than* a value.

$$H_0: \mu \geq \mu_0 \qquad H_a: \mu < \mu_0$$

**How to choose:** Let the business question guide you. If the question is "Has average wait time changed?" → two-tailed. If the question is "Has average wait time decreased (improved)?" → left-tailed. If the question is "Has the defect rate exceeded the specification?" → right-tailed.

### Step 2: Set the Significance Level

The **significance level** ($\alpha$, "alpha") is the probability of rejecting $H_0$ when it is actually true — a false positive. Common choices: $\alpha = 0.05$ (5%) or $\alpha = 0.01$ (1%). The analyst sets $\alpha$ **before** looking at the data.

A smaller $\alpha$ means stronger evidence is required to reject $H_0$. In high-stakes decisions (medical devices, aviation safety), $\alpha = 0.01$ or smaller is appropriate.

## Type I and Type II Errors

Hypothesis testing can lead to two types of errors:

| | $H_0$ is actually TRUE | $H_0$ is actually FALSE |
|--|----------------------|------------------------|
| **Reject $H_0$** | Type I Error (False Positive) | Correct Decision |
| **Fail to Reject $H_0$** | Correct Decision | Type II Error (False Negative) |

**Type I Error:** Rejecting a true null hypothesis. Probability = $\alpha$ (the significance level). This is the probability of a false alarm.

**Type II Error:** Failing to reject a false null hypothesis. Probability = $\beta$ ("beta"). This is the probability of missing a real effect.

**Business framing of error costs:**

- **Type I Error cost in quality control:** Stopping a production line that is actually running fine — wasting time and money.
- **Type II Error cost in quality control:** Allowing a defective production run to pass — producing bad products, damaging customer relationships.

- **Type I Error in drug testing:** Approving a drug that is actually ineffective — patients receive an ineffective treatment.
- **Type II Error in drug testing:** Rejecting a drug that is actually effective — patients miss out on a beneficial treatment.

The costs of each error type guide the choice of $\alpha$. When Type I errors are very costly, set $\alpha$ small. When Type II errors are very costly, you may need a larger $\alpha$ (or a larger sample size, which reduces $\beta$).

### Step 3: Compute the Test Statistic

A **test statistic** is a numerical value computed from sample data that measures how far the sample result is from what we would expect if $H_0$ were true. Larger absolute values of the test statistic provide more evidence against $H_0$.

### Step 4: Find the P-value

The **p-value** is the probability of obtaining a sample result at least as extreme as the one observed, **assuming $H_0$ is true**. It quantifies the strength of evidence against $H_0$.

- A small p-value means the observed data would be very unlikely if $H_0$ were true — this is evidence against $H_0$.
- A large p-value means the observed data is consistent with $H_0$ — no strong evidence to reject it.

<div class="callout note-box">
<span class="callout-title">Note</span>
The p-value is **not** the probability that $H_0$ is true. It is the probability of the data (or more extreme data) given that $H_0$ is true. This distinction is subtle but important. A p-value of 0.03 does not mean there is a 3% chance the null hypothesis is correct — it means that if the null hypothesis were correct, there would be only a 3% chance of observing data as extreme as what we observed.
</div>

### Step 5: Make a Decision

**Decision rule:**
- If $p\text{-value} \leq \alpha$: **Reject $H_0$**. The data provides sufficient evidence to support $H_a$.
- If $p\text{-value} > \alpha$: **Fail to reject $H_0$**. The data does not provide sufficient evidence to reject $H_0$.

<div class="callout warning-box">
<span class="callout-title">Caution</span>
We **never** "accept" $H_0$. Failing to reject $H_0$ does not prove it is true — it simply means we don't have enough evidence to reject it. The correct language is always "fail to reject $H_0$," not "accept $H_0$." This is a crucial distinction in scientific and business communication.
</div>

## Z-Test for a Population Mean (σ Known)

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Z-test statistic for $\mu$ when $\sigma$ is known:**
$$Z = \frac{\bar{x} - \mu_0}{\sigma / \sqrt{n}}$$

where $\mu_0$ is the hypothesized value of $\mu$ from $H_0$.

Under $H_0$, this statistic follows a standard normal distribution.
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Z-Test Example: Fill Volume Quality Control**

A beverage company's machines are supposed to fill cans to exactly $\mu_0 = 355$ mL. The population standard deviation is known to be $\sigma = 4$ mL. A quality control inspector samples $n = 36$ cans and finds $\bar{x} = 353.2$ mL. At $\alpha = 0.05$, does the evidence suggest the machine is not filling to the target volume?

**Step 1:** $H_0: \mu = 355$ mL; $H_a: \mu \neq 355$ mL (two-tailed)

**Step 2:** $\alpha = 0.05$

**Step 3:** $Z = \frac{353.2 - 355}{4/\sqrt{36}} = \frac{-1.8}{0.667} = -2.70$

**Step 4:** For a two-tailed test, p-value = $2 \times P(Z \leq -2.70) = 2 \times 0.0035 = 0.0070$

**Step 5:** Since p-value ($0.007$) < $\alpha$ ($0.05$), **reject $H_0$**.

**Conclusion:** There is sufficient evidence at the 5% significance level that the machine is not filling cans to the target volume of 355 mL.
</div>

## t-Test for a Population Mean (σ Unknown)

In practice, $\sigma$ is unknown. We use the sample standard deviation $s$ and the t-distribution.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**t-test statistic for $\mu$ when $\sigma$ is unknown:**
$$t = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}$$

with degrees of freedom $df = n - 1$.

**Conditions:** Simple random sample; population approximately normal (always safe) or $n \geq 30$ (CLT).
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**t-Test Example: Customer Wait Time**

A fast-food chain claims its drive-through mean wait time is $\mu_0 = 3.5$ minutes. A competitor's analyst suspects the chain is slower than advertised. She samples $n = 25$ drive-through visits at a specific location and finds $\bar{x} = 4.1$ minutes, $s = 1.2$ minutes. At $\alpha = 0.05$, is there sufficient evidence that the true mean wait time exceeds 3.5 minutes?

**Step 1:** $H_0: \mu \leq 3.5$; $H_a: \mu > 3.5$ (right-tailed)

**Step 2:** $\alpha = 0.05$, $df = 24$

**Step 3:** $t = \frac{4.1 - 3.5}{1.2/\sqrt{25}} = \frac{0.6}{0.24} = 2.50$

**Step 4:** p-value = $P(t_{24} > 2.50)$. In Excel: `=T.DIST.RT(2.50, 24)` = 0.0099

**Step 5:** Since p-value ($0.0099$) < $\alpha$ ($0.05$), **reject $H_0$**.

**Conclusion:** There is sufficient evidence at the 5% level that the mean wait time exceeds 3.5 minutes at this location.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**One-Sample t-Test Functions in Excel:**

Finding p-values for t-tests:
- Two-tailed: `=T.DIST.2T(ABS(t), df)` — Note: always take the absolute value of $t$ for this formula
- Left-tailed: `=T.DIST(t, df, TRUE)`
- Right-tailed: `=T.DIST.RT(t, df)`

Finding critical t values:
- Two-tailed: `=T.INV.2T(alpha, df)` — returns the positive critical value; $H_0$ is rejected if $|t| >$ this value
- Right-tailed: `=T.INV(1-alpha, df)`
- Left-tailed: `=T.INV(alpha, df)`

**Example for the wait time test:**
`=T.DIST.RT(2.50, 24)` → p-value = 0.0099
`=T.INV(0.95, 24)` → critical value = 1.711 (reject $H_0$ if $t > 1.711$; since $t = 2.50 > 1.711$, reject $H_0$ ✓)
</div>

### Using Excel's Data Analysis ToolPak for t-Tests

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Running a One-Sample t-Test in Excel (Data Analysis ToolPak approach):**

Excel's ToolPak does not have a direct one-sample t-test tool, but you can work around this:

**Method:** Enter a column of hypothesized values ($\mu_0$) equal in length to your sample (all the same value), then use the **t-Test: Paired Two Sample for Means** tool in the ToolPak, treating your sample as Variable 1 and the hypothesized column as Variable 2. The resulting t statistic and p-value will be correct for a one-sample t-test.

**Alternatively**, compute directly in cells:
```
=AVERAGE(data)           → sample mean (x-bar)
=STDEV.S(data)          → sample std dev (s)
=COUNT(data)             → n
=(AVERAGE(data)-mu0)/(STDEV.S(data)/SQRT(COUNT(data)))  → t statistic
=T.DIST.RT(t_cell, n-1)  → p-value (right-tailed)
```
</div>

## Z-Test for a Population Proportion

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Z-test statistic for a population proportion $p$:**
$$Z = \frac{\hat{p} - p_0}{\sqrt{p_0(1-p_0)/n}}$$

where $p_0$ is the hypothesized proportion from $H_0$ and $\hat{p}$ is the sample proportion.

**Conditions:** Simple random sample; $np_0 \geq 5$ and $n(1-p_0) \geq 5$.
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Z-Test for Proportion: Customer Defect Rate**

A company's historical defect rate has been $p_0 = 0.04$ (4%). After a process improvement, the quality manager samples 200 items and finds 4 defective items. At $\alpha = 0.05$, does this provide evidence that the defect rate has decreased?

**Step 1:** $H_0: p \geq 0.04$; $H_a: p < 0.04$ (left-tailed)

**Step 2:** $\alpha = 0.05$

$\hat{p} = 4/200 = 0.02$

Check: $200(0.04) = 8 \geq 5$ ✓, $200(0.96) = 192 \geq 5$ ✓

**Step 3:** $Z = \frac{0.02 - 0.04}{\sqrt{0.04 \times 0.96/200}} = \frac{-0.02}{\sqrt{0.000192}} = \frac{-0.02}{0.01386} = -1.443$

**Step 4:** p-value = $P(Z \leq -1.443)$ = `=NORM.S.DIST(-1.443, TRUE)` = 0.0745

**Step 5:** Since p-value ($0.0745$) > $\alpha$ ($0.05$), **fail to reject $H_0$**.

**Conclusion:** The evidence is not quite strong enough at the 5% level to conclude that the defect rate has decreased, though the p-value (0.0745) is relatively low and the improvement is promising. The manager might collect a larger sample to confirm the improvement.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Z-Test for Proportion in Excel:**

Excel does not have a specific proportion Z-test function in the ToolPak, but you can compute it directly:

```
=( phat - p0 ) / SQRT( p0*(1-p0)/n )   → Z statistic

For p-values:
Left-tailed:  =NORM.S.DIST(Z, TRUE)
Right-tailed: =1-NORM.S.DIST(Z, TRUE)
Two-tailed:   =2*NORM.S.DIST(-ABS(Z), TRUE)
```

For the defect rate example:
`=( (4/200) - 0.04 ) / SQRT( 0.04*0.96/200 )` → Z = -1.443
`=NORM.S.DIST(-1.443, TRUE)` → p-value = 0.0745
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Hypothesis Test</dt>
<dd>A statistical procedure for deciding between two competing claims (hypotheses) about a population parameter, based on sample evidence.</dd>

<dt>Null Hypothesis ($H_0$)</dt>
<dd>The default or "status quo" claim about a population parameter; assumed true unless evidence proves otherwise. Always stated with an equals sign.</dd>

<dt>Alternative Hypothesis ($H_a$)</dt>
<dd>The research claim; what the analyst suspects may be true. The conclusion reached if $H_0$ is rejected.</dd>

<dt>Significance Level ($\alpha$)</dt>
<dd>The probability of rejecting a true null hypothesis (Type I error rate); set by the analyst before testing, commonly 0.05 or 0.01.</dd>

<dt>Type I Error</dt>
<dd>Rejecting $H_0$ when it is actually true (a false positive); its probability equals $\alpha$.</dd>

<dt>Type II Error</dt>
<dd>Failing to reject $H_0$ when it is actually false (a false negative); its probability is $\beta$.</dd>

<dt>Test Statistic</dt>
<dd>A value computed from sample data that measures how far the observed result is from the null hypothesis; used to determine the p-value.</dd>

<dt>P-value</dt>
<dd>The probability of observing a sample result at least as extreme as the one obtained, assuming $H_0$ is true. A small p-value is evidence against $H_0$.</dd>

<dt>Reject $H_0$</dt>
<dd>The conclusion when the p-value is less than or equal to $\alpha$; there is sufficient evidence to support $H_a$.</dd>

<dt>Fail to Reject $H_0$</dt>
<dd>The conclusion when the p-value is greater than $\alpha$; insufficient evidence to support $H_a$. This is NOT the same as proving $H_0$ is true.</dd>
</dl>
</div>

---

## Exercises {-}

1. For each scenario, state the appropriate **null and alternative hypotheses** and indicate whether the test is **left-tailed, right-tailed, or two-tailed**:
   a. A bank claims its ATM cash dispensing error is less than \$0.50 per transaction on average. An auditor suspects the error is actually higher.
   b. A pharmaceutical company claims a new pain reliever works in a mean of 45 minutes. Researchers want to determine whether the mean time differs from 45 minutes.
   c. A factory's specification calls for bolts to have a mean diameter of 10 mm. The quality control department checks whether the machine is producing bolts at the specified diameter.
   d. A new training program claims to reduce employee error rates. The HR department tests whether errors have decreased from the previous mean of 3.2 per day.

2. A manager believes the population standard deviation of weekly sales at her stores is $\sigma = \$3,000$. Corporate sets the standard that mean weekly sales should be \$24,500. A sample of 35 weeks shows $\bar{x} = \$23,800$. At $\alpha = 0.05$, test whether mean sales are below the corporate standard.
   a. State $H_0$ and $H_a$.
   b. Compute the Z-test statistic.
   c. Find the p-value.
   d. State your conclusion in plain language.

3. A marketing manager claims that the average time visitors spend on the company website is at least 4 minutes. A sample of 30 visitors shows $\bar{x} = 3.6$ minutes, $s = 1.4$ minutes. Test at $\alpha = 0.01$.
   a. State $H_0$ and $H_a$.
   b. Calculate the t-test statistic and degrees of freedom.
   c. Find the p-value using Excel's `T.DIST` function.
   d. What is your conclusion? What would be the business implication if $H_0$ is rejected?

4. A hotel claims that 90% of guests rate their stay as "Satisfactory" or better. An industry analyst surveys 200 recent guests and finds 172 gave favorable ratings. Test this claim at $\alpha = 0.05$ (two-tailed).
   a. Check the conditions for the proportion Z-test.
   b. Compute $\hat{p}$ and the Z-test statistic.
   c. Find the p-value and state your conclusion.

5. Identify and explain the type of error (Type I or Type II) in each scenario:
   a. A drug company's test concludes that a new medication is effective when in fact it provides no benefit over a placebo.
   b. A quality control test concludes that a production batch is acceptable when it actually contains a high proportion of defective items.
   c. An auditor concludes there is no significant fraud in a financial statement when substantial fraud actually exists.

6. An e-commerce company recently redesigned its checkout process to reduce cart abandonment. The old process had an average cart value of \$85 at time of abandonment. After the redesign, a sample of 48 abandoned carts has $\bar{x} = \$89.50$ and $s = \$18.20$. Test at $\alpha = 0.10$ whether average cart value at abandonment has changed (two-tailed).

7. A call center has a policy that 80% of calls should be resolved on the first attempt ("first-call resolution"). A quality analyst samples 150 calls and finds that 111 were resolved on first contact. At $\alpha = 0.05$, is there evidence that first-call resolution has fallen below the 80% target?

8. *A consumer advocacy group claims that a popular brand of olive oil bottles contains less than the labeled 500 mL on average. They purchase and measure a random sample of 20 bottles: $\bar{x} = 494.2$ mL, $s = 8.4$ mL. At $\alpha = 0.01$, do they have sufficient evidence to support their claim? Discuss both the statistical conclusion and the practical significance of the finding — is a difference of 5.8 mL per bottle a meaningful problem for consumers?*
