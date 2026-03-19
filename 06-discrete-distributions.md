# Discrete Probability Distributions {#discrete}

## From Events to Distributions

In Chapter 5, we computed the probability of a single event. In practice, we often want to understand an entire pattern of possible outcomes and their associated probabilities. A **probability distribution** provides exactly this — a complete picture of all possible values a variable can take and how likely each value is.

This chapter focuses on **discrete probability distributions**, which describe variables that take on a countable number of distinct values. We develop three important distributions: the general discrete distribution, the binomial distribution, and the Poisson distribution — all with direct business applications.

## Random Variables

A **random variable** is a variable whose value is determined by the outcome of a probability experiment. We use uppercase letters (like $X$) to denote random variables and lowercase letters (like $x$) for specific values they take.

There are two types of random variables:

**Discrete random variables** take on a countable number of distinct values — typically whole numbers or a finite set of outcomes. The key word is *countable*: you can list all possible values.

Examples:
- Number of customers arriving at a bank in one hour (0, 1, 2, 3, …)
- Number of defective items in a batch of 50
- Number of insurance claims filed in a week
- Number of job applicants interviewed before making a hire

**Continuous random variables** can take any value within a range — any real number within an interval, including fractions. They arise from measurements.

Examples:
- Time to complete a service transaction (any positive real number)
- Daily stock return (-∞ to +∞ in theory)
- Weight of a shipped package
- Temperature in a warehouse

The distinction matters because the mathematical treatment is different. In this chapter, we focus on discrete random variables. Continuous random variables are covered in Chapter 7.

## Probability Distribution Tables

For a discrete random variable $X$, a **probability distribution** is a table (or formula) that lists every possible value $x$ and its corresponding probability $P(X = x)$.

**Requirements for a valid probability distribution:**
1. $P(X = x) \geq 0$ for all $x$ (probabilities cannot be negative)
2. $\sum_{\text{all } x} P(X = x) = 1$ (all probabilities sum to 1)

<div class="callout example-box">
<span class="callout-title">Example</span>
**Number of Complaints per Day**

A bank branch tracks the number of customer complaints ($X$) received per day. Based on 200 days of records:

| $x$ | Frequency | $P(X = x)$ |
|-----|-----------|------------|
| 0 | 60 | 60/200 = 0.30 |
| 1 | 80 | 80/200 = 0.40 |
| 2 | 40 | 40/200 = 0.20 |
| 3 | 14 | 14/200 = 0.07 |
| 4 | 6 | 6/200 = 0.03 |
| **Total** | **200** | **1.00** |

Verification: $0.30 + 0.40 + 0.20 + 0.07 + 0.03 = 1.00$ ✓

From this table: $P(X = 2) = 0.20$, $P(X \leq 1) = 0.30 + 0.40 = 0.70$, $P(X \geq 3) = 0.07 + 0.03 = 0.10$.
</div>

## Expected Value (Mean) of a Discrete Distribution

The **expected value** of a discrete random variable, written $E(X)$ or $\mu$, is the long-run average value if the experiment were repeated many times. It is a weighted average of all possible values, where the weights are the probabilities.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$E(X) = \mu = \sum_{\text{all } x} x \cdot P(X = x)$$
</div>

Using the complaints example:
$$\mu = 0(0.30) + 1(0.40) + 2(0.20) + 3(0.07) + 4(0.03)$$
$$= 0 + 0.40 + 0.40 + 0.21 + 0.12 = 1.13$$

The bank branch receives, on average, **1.13 complaints per day**. This is a long-run average — on any given day you cannot have 1.13 complaints, but the average over many days is 1.13.

## Variance and Standard Deviation of a Discrete Distribution

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Variance of a discrete random variable:**
$$\sigma^2 = \text{Var}(X) = \sum_{\text{all } x} (x - \mu)^2 \cdot P(X = x)$$

**Standard deviation:**
$$\sigma = \sqrt{\sigma^2}$$
</div>

Continuing the complaints example ($\mu = 1.13$):

| $x$ | $P(X=x)$ | $(x-\mu)$ | $(x-\mu)^2$ | $(x-\mu)^2 \cdot P(X=x)$ |
|-----|-----------|-----------|-------------|--------------------------|
| 0 | 0.30 | -1.13 | 1.2769 | 0.3831 |
| 1 | 0.40 | -0.13 | 0.0169 | 0.0068 |
| 2 | 0.20 | 0.87 | 0.7569 | 0.1514 |
| 3 | 0.07 | 1.87 | 3.4969 | 0.2448 |
| 4 | 0.03 | 2.87 | 8.2369 | 0.2471 |
| **Total** | | | | **1.0332** |

$\sigma^2 = 1.0332$, $\sigma = \sqrt{1.0332} \approx 1.016$

The standard deviation of daily complaints is approximately **1.016 complaints**.

## Expected Value in Business Decision Making

Expected value is one of the most powerful tools in business decision analysis. When comparing options under uncertainty, the option with the highest expected value is generally preferable (assuming risk neutrality).

<div class="callout example-box">
<span class="callout-title">Example</span>
**Product Launch Decision**

A company is deciding whether to launch a new product. The outcomes and their probabilities depend on market conditions:

| Market Outcome | Probability | Profit (Loss) |
|---------------|-------------|---------------|
| Strong demand | 0.30 | \$800,000 |
| Moderate demand | 0.45 | \$200,000 |
| Weak demand | 0.25 | -\$300,000 |

Expected profit = $0.30(800,000) + 0.45(200,000) + 0.25(-300,000)$
$= 240,000 + 90,000 - 75,000 = \$255,000$

The expected profit is **\$255,000**. If the company does not launch, the profit is \$0. Based on expected value, launching is the better decision.

However, note that there is a 25% chance of losing \$300,000. A risk-averse decision maker might weigh this downside risk and choose not to launch, even though the expected value favors launching. Expected value is a useful starting point, but it does not capture the full picture of risk tolerance.
</div>

## The Binomial Distribution

The **binomial distribution** is one of the most important and widely used discrete probability distributions in business. It applies when an experiment consists of a fixed number of **identical, independent trials**, each with only two possible outcomes.

### Conditions for a Binomial Distribution

An experiment follows a binomial distribution if ALL four conditions are met:
1. The experiment consists of **$n$ identical trials**.
2. Each trial has only **two possible outcomes**: "success" (what we're counting) or "failure."
3. The probability of success, $p$, is **constant from trial to trial**.
4. The trials are **independent** (the outcome of one trial does not affect others).

Business examples where binomial applies:
- Randomly selecting 20 customer orders; each is either correct or incorrect.
- Calling 50 potential donors; each either donates or doesn't.
- Testing 100 manufactured items; each is either defective or not.
- Sending 30 job offers; each candidate either accepts or declines.

### Binomial Probability Formula

<div class="callout formula-box">
<span class="callout-title">Formula</span>
If $X$ is the number of successes in $n$ trials with success probability $p$ per trial:

$$P(X = x) = \binom{n}{x} p^x (1-p)^{n-x}$$

where $\binom{n}{x} = \dfrac{n!}{x!(n-x)!}$ is the number of ways to choose $x$ successes from $n$ trials (combinations).

**Mean and standard deviation of the binomial distribution:**
$$\mu = np \qquad \sigma = \sqrt{np(1-p)}$$
</div>

The notation $n!$ (read "n factorial") means $n \times (n-1) \times (n-2) \times \cdots \times 1$. For example, $5! = 5 \times 4 \times 3 \times 2 \times 1 = 120$. Note: $0! = 1$ by convention.

<div class="callout example-box">
<span class="callout-title">Example</span>
**Quality Control — Binomial Application**

A supplier historically delivers about 8% defective parts. A manufacturer receives a shipment and randomly inspects 15 parts. Let $X$ = number of defective parts found.

Here: $n = 15$, $p = 0.08$, $(1-p) = 0.92$.

**What is the probability that exactly 2 of the 15 parts are defective?**

$$P(X = 2) = \binom{15}{2}(0.08)^2(0.92)^{13}$$

$\binom{15}{2} = \frac{15!}{2! \times 13!} = \frac{15 \times 14}{2} = 105$

$(0.08)^2 = 0.0064$

$(0.92)^{13} \approx 0.3530$

$$P(X = 2) = 105 \times 0.0064 \times 0.3530 \approx 0.2370$$

There is approximately a **23.7% chance** of finding exactly 2 defective parts.

Mean: $\mu = 15 \times 0.08 = 1.2$ defective parts expected.
Standard deviation: $\sigma = \sqrt{15 \times 0.08 \times 0.92} = \sqrt{1.104} \approx 1.05$
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Using BINOM.DIST in Excel:**

`=BINOM.DIST(x, n, p, cumulative)`

- `x` = number of successes
- `n` = number of trials
- `p` = probability of success per trial
- `cumulative` = FALSE for exact probability $P(X = x)$; TRUE for cumulative probability $P(X \leq x)$

**Examples:**
- $P(X = 2)$ with $n=15$, $p=0.08$: `=BINOM.DIST(2, 15, 0.08, FALSE)` → 0.2369
- $P(X \leq 2)$ with $n=15$, $p=0.08$: `=BINOM.DIST(2, 15, 0.08, TRUE)` → 0.8041
- $P(X \geq 3)$ with $n=15$, $p=0.08$: `=1-BINOM.DIST(2, 15, 0.08, TRUE)` → 0.1959

**Tip:** To find $P(X \geq k)$, use `=1-BINOM.DIST(k-1, n, p, TRUE)`.
</div>

## The Poisson Distribution

The **Poisson distribution** models the number of times a random event occurs within a fixed interval of time or space, when events happen independently and at a constant average rate.

### Conditions for a Poisson Distribution

1. Events occur **randomly and independently**.
2. The average rate of events ($\lambda$, "lambda") is **constant** over the interval.
3. Two events cannot occur at **exactly the same instant** (for time-based processes).

Business examples where Poisson applies:
- Number of customers arriving at a bank in 15-minute intervals
- Number of accidents at a warehouse per month
- Number of machine breakdowns per week
- Number of phone calls received by a call center per hour
- Number of typos per page in a document

### Poisson Probability Formula

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$P(X = x) = \frac{e^{-\lambda} \lambda^x}{x!}$$

where:
- $x = 0, 1, 2, 3, \ldots$ (number of events)
- $\lambda$ = average number of events in the interval (a positive number)
- $e \approx 2.71828$ (the base of natural logarithms)

**Mean and standard deviation of the Poisson distribution:**
$$\mu = \lambda \qquad \sigma = \sqrt{\lambda}$$

A remarkable property: the mean and variance are both equal to $\lambda$.
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Customer Arrivals — Poisson Application**

A coffee shop averages 12 customers arriving per 30-minute interval during the morning rush. The manager wants to staff appropriately. Let $X$ = number of customers in a 30-minute interval. Here $\lambda = 12$.

**What is the probability that exactly 10 customers arrive in a 30-minute interval?**

$$P(X = 10) = \frac{e^{-12}(12)^{10}}{10!} = \frac{(6.144 \times 10^{-6})(61,917,364,224)}{3,628,800} \approx 0.1048$$

There is approximately a **10.5%** chance that exactly 10 customers arrive.

Note: This calculation is tedious by hand; use Excel's `POISSON.DIST` function in practice.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Using POISSON.DIST in Excel:**

`=POISSON.DIST(x, lambda, cumulative)`

- `x` = number of events
- `lambda` = average rate ($\lambda$)
- `cumulative` = FALSE for exact $P(X = x)$; TRUE for cumulative $P(X \leq x)$

**Examples** (with $\lambda = 12$):
- $P(X = 10)$: `=POISSON.DIST(10, 12, FALSE)` → 0.1048
- $P(X \leq 10)$: `=POISSON.DIST(10, 12, TRUE)` → 0.3472
- $P(X > 15)$: `=1-POISSON.DIST(15, 12, TRUE)` → 0.1550

**Scaling the rate:** If events average 12 per 30 minutes, then for a 15-minute interval, use $\lambda = 6$. Always match $\lambda$ to the length of your specific interval.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Random Variable</dt>
<dd>A variable whose numerical value is determined by the outcome of a probability experiment.</dd>

<dt>Discrete Random Variable</dt>
<dd>A random variable that can take on a countable number of distinct values.</dd>

<dt>Continuous Random Variable</dt>
<dd>A random variable that can take any value in a continuous range; arises from measurements.</dd>

<dt>Probability Distribution</dt>
<dd>A listing (or formula) of all possible values of a random variable and their associated probabilities.</dd>

<dt>Expected Value $E(X)$</dt>
<dd>The long-run average value of a random variable; computed as a probability-weighted sum of all possible values.</dd>

<dt>Variance $\sigma^2$</dt>
<dd>The expected value of the squared deviations from the mean of a probability distribution.</dd>

<dt>Binomial Distribution</dt>
<dd>A discrete probability distribution for the number of successes in $n$ independent, identical trials, each with probability of success $p$.</dd>

<dt>Poisson Distribution</dt>
<dd>A discrete probability distribution for the number of events occurring in a fixed time or space interval, given a constant average rate $\lambda$.</dd>

<dt>$\lambda$ (lambda)</dt>
<dd>The average rate of occurrences per interval in a Poisson distribution; also equals the mean and variance of the distribution.</dd>
</dl>
</div>

---

## Exercises {-}

1. A convenience store tracks the number of customers ($X$) who visit during the slow midday hour. Over 100 days, the data shows: 0 customers (10 days), 1 customer (25 days), 2 customers (30 days), 3 customers (20 days), 4 customers (15 days).
   a. Construct the **probability distribution table** for $X$.
   b. Verify that probabilities sum to 1.
   c. Compute $E(X)$ and interpret it.
   d. Compute $\text{Var}(X)$ and $\sigma$.

2. An insurance company offers a one-year home warranty policy for \$450. Historical data shows the following payout amounts and their probabilities:

   | Payout | Probability |
   |--------|-------------|
   | \$0 (no claim) | 0.72 |
   | \$500 | 0.15 |
   | \$1,500 | 0.09 |
   | \$5,000 | 0.04 |

   a. Compute the **expected payout** per policy.
   b. If the premium is \$450, what is the company's expected **profit per policy**?
   c. What is the **standard deviation** of payouts?

3. A sales representative makes 12 cold calls per day. Based on past experience, each call results in a scheduled meeting with probability 0.20, independently of other calls. Let $X$ = number of meetings scheduled per day.
   a. State why this is a **binomial** situation. Verify all four conditions.
   b. Find $\mu$ and $\sigma$ for $X$.
   c. Use Excel's `BINOM.DIST` to find: $P(X = 3)$, $P(X \leq 2)$, and $P(X \geq 4)$.

4. A quality inspector samples 20 circuit boards from a production run. The process has a known defect rate of 5%. Let $X$ = number of defective boards in the sample.
   a. Find the **probability that no boards are defective**.
   b. Find the **probability that at most 2 boards are defective**.
   c. Find the **probability that more than 3 boards are defective**.
   d. If the inspector finds 6 defective boards, should she be concerned that the defect rate has risen above 5%? Compute $P(X \geq 6)$ and use it to support your answer.

5. A hospital emergency room receives an average of 4 patients per hour during the overnight shift. Assume the number of arrivals follows a Poisson distribution with $\lambda = 4$ per hour.
   a. Find the probability that exactly **3 patients** arrive in a given hour.
   b. Find the probability that **6 or more patients** arrive in a given hour.
   c. The ER has sufficient staff to handle up to 7 patients per hour. Find the probability that staffing will be **insufficient** in any given hour.
   d. What is the average and standard deviation of patients per hour?

6. *A loan officer at a community bank reviews 15 loan applications per week. Each application has a 30% probability of being declined. Assume independence.*
   a. *On average, how many applications will be declined per week?*
   b. *Find the probability that exactly 5 are declined.*
   c. *Find the probability that more than half (more than 7) are declined. What does this probability suggest about the rarity of this event?*
   d. *If the bank's policy requires review by a supervisor when 8 or more applications are declined in a week, what is the probability that supervisor review will be needed?*
