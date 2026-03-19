# The Normal Distribution {#normal}

## The Most Important Distribution in Statistics

If there is one distribution that every business statistics student must understand deeply, it is the **normal distribution**. Also called the **bell curve** or Gaussian distribution, it appears naturally in an enormous range of business and natural phenomena: employee heights, manufacturing tolerances, test scores, financial returns, measurement errors, and countless others.

More importantly, the normal distribution underlies virtually all of the inferential methods in the second half of this course. Understanding it thoroughly is the key that unlocks confidence intervals, hypothesis tests, and regression inference.

## Properties of the Normal Distribution

A **normal distribution** is a continuous probability distribution characterized by a symmetric, bell-shaped curve. Its key properties:

1. **Bell-shaped and symmetric** about the mean $\mu$. The left and right halves of the curve are mirror images.
2. **Defined by two parameters:** the mean $\mu$ (which determines the center) and the standard deviation $\sigma$ (which determines the spread).
3. **The mean, median, and mode are all equal** — they coincide at the center of the distribution.
4. **The curve extends from $-\infty$ to $+\infty$** — it never actually touches the horizontal axis (called an asymptote), though the probability becomes negligible beyond three standard deviations from the mean.
5. **The total area under the curve equals 1** (since it represents total probability = 100%).
6. **The Empirical Rule applies:** approximately 68%, 95%, and 99.7% of values fall within 1, 2, and 3 standard deviations of the mean.

Changing $\mu$ shifts the curve left or right. Changing $\sigma$ makes the curve wider (larger $\sigma$) or narrower (smaller $\sigma$) — but the total area always remains 1.

## The Standard Normal Distribution

There are infinitely many normal distributions (one for each combination of $\mu$ and $\sigma$). Rather than creating a separate probability table for every possible normal distribution, statisticians work with a single **standard normal distribution**, which has:

$$\mu = 0 \qquad \sigma = 1$$

The standard normal distribution is denoted $Z$. Its horizontal axis is labeled in **Z-scores** (also called standard scores).

## Z-Scores

A **Z-score** measures how many standard deviations a value $x$ is above or below the mean of its distribution.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Converting a raw value to a Z-score:**
$$Z = \frac{x - \mu}{\sigma}$$

- A positive Z-score means $x$ is above the mean.
- A negative Z-score means $x$ is below the mean.
- $Z = 0$ means $x$ equals the mean.
- $|Z| = 1$ means $x$ is exactly one standard deviation from the mean.
</div>

**Interpreting Z-scores in business:**
- An employee's salary has Z-score = +2.1: the salary is 2.1 standard deviations above the mean for that role. It is unusually high.
- A product's weight has Z-score = -0.3: the weight is 0.3 standard deviations below the target weight. It is close to target.
- A store's monthly sales have Z-score = +3.5: sales are 3.5 standard deviations above average — an exceptionally strong month.

<div class="callout example-box">
<span class="callout-title">Example</span>
**Standardizing Exam Scores**

A business statistics exam had a mean score of $\mu = 72$ and a standard deviation of $\sigma = 9$. Student A scored 87; Student B scored 63.

Student A: $Z_A = \frac{87 - 72}{9} = \frac{15}{9} \approx 1.67$ (1.67 standard deviations above the mean)

Student B: $Z_B = \frac{63 - 72}{9} = \frac{-9}{9} = -1.00$ (1.00 standard deviation below the mean)
</div>

## Finding Probabilities Using Z-Scores

Once we convert a value to a Z-score, we can find the probability that a normally distributed variable falls below, above, or between specific values. The probability corresponds to the **area under the normal curve**.

### Using Standard Normal Tables

A standard normal table (also called a Z-table) gives $P(Z \leq z)$ — the cumulative probability from the far left of the distribution up to the value $z$.

**Example:** $P(Z \leq 1.67) = ?$
Look up 1.6 in the row and 0.07 in the column: $P(Z \leq 1.67) \approx 0.9525$.

About 95.25% of values in a normal distribution fall below a Z-score of 1.67.

**Useful tricks with the Z-table:**
- For $P(Z > z)$: use $1 - P(Z \leq z)$ (complement rule)
- For $P(Z \leq -z)$: use symmetry: $P(Z \leq -z) = P(Z \geq z) = 1 - P(Z \leq z)$
- For $P(a \leq Z \leq b)$: use $P(Z \leq b) - P(Z \leq a)$

### Using Excel for Normal Probabilities

Excel makes normal probability calculations much faster and more precise than tables.

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Normal Distribution Functions in Excel:**

`=NORM.S.DIST(z, cumulative)` — Standard normal distribution
- `z` = the Z-score
- `cumulative` = TRUE for $P(Z \leq z)$; FALSE for the height of the curve at $z$ (rarely needed)

`=NORM.DIST(x, mean, std_dev, cumulative)` — Normal distribution for any $\mu$ and $\sigma$
- `x` = the raw value (no need to compute Z first!)
- `mean` = $\mu$
- `std_dev` = $\sigma$
- `cumulative` = TRUE for $P(X \leq x)$

**Examples:**
- $P(Z \leq 1.67)$: `=NORM.S.DIST(1.67, TRUE)` → 0.9525
- $P(Z > 1.67)$: `=1-NORM.S.DIST(1.67, TRUE)` → 0.0475
- $P(-1 \leq Z \leq 2)$: `=NORM.S.DIST(2,TRUE)-NORM.S.DIST(-1,TRUE)` → 0.8186
- $P(X \leq 87)$ with $\mu=72$, $\sigma=9$: `=NORM.DIST(87, 72, 9, TRUE)` → 0.9525
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Quality Control — Finding Defect Probabilities**

A packaging machine fills bags of coffee beans. The fill weight is normally distributed with $\mu = 16.0$ oz and $\sigma = 0.25$ oz.

**What proportion of bags are underfilled (below 15.5 oz)?**

Method 1 (Z-score + table): $Z = \frac{15.5 - 16.0}{0.25} = \frac{-0.5}{0.25} = -2.00$
$P(Z < -2.00) = 0.0228$ → About 2.28% of bags are underfilled.

Method 2 (Excel directly): `=NORM.DIST(15.5, 16.0, 0.25, TRUE)` → 0.0228

**What proportion of bags weigh between 15.6 oz and 16.4 oz?**

$Z_1 = (15.6 - 16.0)/0.25 = -1.60$, $Z_2 = (16.4 - 16.0)/0.25 = 1.60$

$P(-1.60 \leq Z \leq 1.60) = P(Z \leq 1.60) - P(Z \leq -1.60) = 0.9452 - 0.0548 = 0.8904$

In Excel: `=NORM.DIST(16.4,16,0.25,TRUE)-NORM.DIST(15.6,16,0.25,TRUE)` → 0.8904

About **89.04%** of bags fall within this acceptable range.
</div>

## Finding Values from Probabilities (Inverse Normal)

Sometimes we work **backward**: given a probability, find the corresponding value $x$ or Z-score. This is called the **inverse normal** problem.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
If we know $P(X \leq x) = p$ and we want to find $x$:

Using a Z-table: find the Z-score corresponding to probability $p$, then convert back:
$$x = \mu + Z \cdot \sigma$$
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Inverse Normal Functions in Excel:**

`=NORM.S.INV(probability)` — Finds the Z-score for a given cumulative probability in the standard normal.

`=NORM.INV(probability, mean, std_dev)` — Finds the $x$-value for a given cumulative probability directly.

**Examples:**
- Find $Z$ such that $P(Z \leq z) = 0.95$: `=NORM.S.INV(0.95)` → 1.6449
- Find $Z$ such that $P(Z \leq z) = 0.025$: `=NORM.S.INV(0.025)` → -1.9600
- Find bag weight at 5th percentile with $\mu=16$, $\sigma=0.25$: `=NORM.INV(0.05, 16, 0.25)` → 15.589 oz
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Setting Performance Standards**

A company wants to classify the top 10% of sales representatives as "Elite" performers. Annual sales are normally distributed with $\mu = \$480,000$ and $\sigma = \$62,000$. What minimum sales level qualifies for Elite status?

We need $x$ such that $P(X \geq x) = 0.10$, meaning $P(X \leq x) = 0.90$.

In Excel: `=NORM.INV(0.90, 480000, 62000)` → **\$559,475**

A sales representative must generate at least \$559,475 in annual sales to be classified as Elite.
</div>

## Business Applications of the Normal Distribution

### Quality Control

Manufacturing specifications define acceptable ranges for product dimensions or weights. If the process is normally distributed, we can calculate what percentage of output falls within specs — and what percentage must be scrapped or reworked.

### Financial Returns

Daily, monthly, or annual returns on financial assets are often modeled as approximately normal. This allows risk managers to compute **Value at Risk (VaR)** — the maximum loss expected at a given confidence level (e.g., "We expect to lose no more than \$2 million on 95% of trading days").

<div class="callout example-box">
<span class="callout-title">Example</span>
**Value at Risk**

A portfolio has daily returns that are approximately normal with $\mu = 0.05\%$ and $\sigma = 1.2\%$.

Find the 5th percentile of daily returns (the worst expected loss on 5% of trading days):

`=NORM.INV(0.05, 0.0005, 0.012)` → approximately **-1.924%**

On 95% of trading days, the portfolio loss does not exceed 1.924%. On 5% of days, it does — this is the Value at Risk at the 95% confidence level.
</div>

### Employee Assessment

Human performance metrics (test scores, productivity rates, error rates) often follow approximate normal distributions, making normal probability calculations useful for HR analytics: "What percentage of applicants scoring above X on an assessment are likely to succeed?" or "What training intervention is needed to bring the bottom 20% of performers up to standard?"

## Normal Approximation to the Binomial

When the number of trials $n$ is large, computing binomial probabilities by hand becomes very tedious. Fortunately, if both $np \geq 5$ and $n(1-p) \geq 5$, the binomial distribution is approximately normal with:

$$\mu = np \qquad \sigma = \sqrt{np(1-p)}$$

You can then use normal distribution calculations (Z-scores or Excel's `NORM.DIST`) to approximate binomial probabilities without computing individual binomial terms.

<div class="callout note-box">
<span class="callout-title">Note</span>
The rule of thumb $np \geq 5$ **and** $n(1-p) \geq 5$ ensures that the binomial distribution is sufficiently symmetric and spread for the normal approximation to work well. If either condition is violated — for example, when $p$ is very small or very large — the binomial distribution is too skewed for the normal approximation to be accurate. Use `BINOM.DIST` directly instead.
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Normal Approximation to Binomial**

A call center has 200 agents. Each agent has a 60% chance of meeting their daily performance target, independently. What is the probability that at least 130 agents meet their target today?

$n = 200$, $p = 0.60$. Check: $np = 120 \geq 5$, $n(1-p) = 80 \geq 5$ ✓

Using the normal approximation: $\mu = 200(0.60) = 120$, $\sigma = \sqrt{200(0.60)(0.40)} = \sqrt{48} \approx 6.93$

$P(X \geq 130) \approx P\left(Z \geq \frac{130 - 120}{6.93}\right) = P(Z \geq 1.44) = 1 - 0.9251 = 0.0749$

There is approximately a **7.5%** chance that 130 or more agents meet their target. (Excel's exact answer using `BINOM.DIST`: 0.0762 — very close!)
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Normal Distribution</dt>
<dd>A continuous probability distribution characterized by a symmetric, bell-shaped curve, defined by mean $\mu$ and standard deviation $\sigma$.</dd>

<dt>Standard Normal Distribution</dt>
<dd>A normal distribution with mean $\mu = 0$ and standard deviation $\sigma = 1$; used as the reference for all normal probability calculations.</dd>

<dt>Z-Score (Standard Score)</dt>
<dd>The number of standard deviations a value falls above or below the mean: $Z = (x - \mu)/\sigma$.</dd>

<dt>Cumulative Probability</dt>
<dd>The probability that a random variable takes a value less than or equal to a specified value; the area under the curve to the left of that value.</dd>

<dt>Inverse Normal</dt>
<dd>Finding the value $x$ (or Z-score) that corresponds to a given cumulative probability; the reverse of a probability lookup.</dd>

<dt>Normal Approximation to the Binomial</dt>
<dd>Using the normal distribution to approximate binomial probabilities when $n$ is large and both $np \geq 5$ and $n(1-p) \geq 5$.</dd>

<dt>Value at Risk (VaR)</dt>
<dd>A financial risk measure representing the maximum expected loss at a given confidence level over a given time horizon.</dd>
</dl>
</div>

---

## Exercises {-}

1. The daily number of transactions processed by a bank's online system is normally distributed with $\mu = 8,500$ and $\sigma = 600$.
   a. What is the probability that fewer than 7,800 transactions occur on a given day?
   b. What is the probability that more than 9,500 transactions occur?
   c. What is the probability that transactions fall between 8,000 and 9,200?
   d. Find the 90th percentile — the transaction volume that is exceeded only 10% of days.

2. A candy bar manufacturer fills bars to a mean weight of 45 g with a standard deviation of 1.5 g (normally distributed).
   a. FDA regulations require that no more than 2.5% of bars weigh less than the stated weight of 42.5 g. Does this process meet the regulation? Show your calculation.
   b. What fill mean $\mu$ would the company need to achieve to ensure only 1% of bars are below 42.5 g, keeping $\sigma = 1.5$ g constant?
   c. A bar is selected at random. What is the probability it weighs more than 48 g?

3. Annual salaries for data analysts at a technology firm are normally distributed with $\mu = \$72,000$ and $\sigma = \$8,500$.
   a. What proportion of analysts earn more than \$85,000?
   b. The firm wants to designate the top 15% of earners as "Senior" for a new pay scale. What minimum salary defines the Senior tier?
   c. HR is reviewing salaries below the 10th percentile for potential equity adjustments. What is the 10th percentile salary?

4. An investment fund has monthly returns that are approximately normally distributed with a mean of 0.8% and standard deviation of 2.4%.
   a. In what percentage of months does the fund **lose money** (return < 0%)?
   b. What is the probability the fund gains more than 5% in a given month?
   c. What monthly return represents the **1st percentile** (i.e., the worst 1% of months)?

5. Calculate the following Z-scores and interpret each in context:
   a. A product dimension measures 12.4 cm. The process is set to $\mu = 12.0$ cm with $\sigma = 0.3$ cm.
   b. A call is resolved in 8.5 minutes. Average handle time is $\mu = 6.2$ minutes, $\sigma = 1.8$ minutes.
   c. Monthly store sales are \$124,000. The company average is $\mu = \$138,000$ with $\sigma = \$21,000$.

6. A nationwide standardized test for entry-level accounting positions has scores normally distributed with $\mu = 500$ and $\sigma = 80$.
   a. A company will interview only candidates scoring in the top 20%. What is the minimum qualifying score?
   b. Another company rejects candidates scoring below the 25th percentile. What is the cutoff score?
   c. What percentage of candidates score between 420 and 620?

7. A retailer tracks daily sales (in units) for a popular product. Over the past year (365 days), sales average $\mu = 48$ units with $\sigma = 12$ units.
   a. On how many days would you expect sales to exceed 60 units?
   b. The retailer keeps 80 units in daily safety stock. What is the probability of a stockout (daily demand exceeds 80 units)?
   c. To maintain a 99% service level (stockout probability ≤ 1%), how many units should the daily safety stock be?

8. *A large call center employs 300 agents. Each agent independently has a probability of 0.65 of being "fully engaged" (meeting all performance metrics) in any given week. Check whether the normal approximation to the binomial is appropriate. Then use the normal approximation to find the probability that at least 210 agents are fully engaged in a given week.*
