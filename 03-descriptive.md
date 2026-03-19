# Descriptive Statistics {#descriptive}

## From Data to Understanding

Suppose a regional manager for a clothing retailer receives a spreadsheet with the daily sales revenue for all 35 stores in her district over the past month — 35 stores times 30 days equals 1,050 individual data points. She cannot possibly absorb 1,050 numbers at a glance. She needs a summary. She needs descriptive statistics.

Descriptive statistics are the numerical and graphical tools that take a large pile of numbers and condense them into a compact, meaningful summary. A good summary captures two essential things: **where the data tends to be centered** (measures of central tendency) and **how spread out the data is** (measures of variability).

In this chapter, we develop the most important tools in each category, learn when to use each one, and practice computing them in Excel.

## Measures of Central Tendency

A measure of central tendency is a single number that represents the "typical" or "middle" value of a data set. The three most common measures are the **mean**, the **median**, and the **mode**.

### The Mean

The **arithmetic mean** (often called simply the **mean** or the **average**) is the sum of all values divided by the number of values.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Sample mean:**
$$\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n} = \frac{x_1 + x_2 + \cdots + x_n}{n}$$

where $x_i$ represents each individual value and $n$ is the number of values in the sample.

**Population mean:**
$$\mu = \frac{\sum_{i=1}^{N} x_i}{N}$$

where $N$ is the total number of values in the population.
</div>

**Example:** A small marketing agency tracks the number of new client inquiries it receives each week for six weeks: 14, 19, 22, 18, 25, 16.

$$\bar{x} = \frac{14 + 19 + 22 + 18 + 25 + 16}{6} = \frac{114}{6} = 19$$

The mean number of weekly inquiries is 19.

**When to use the mean:** The mean is the most widely used measure of center because it uses every data value in its calculation. It is appropriate for **ratio or interval data** without extreme outliers. It is the foundation of many other statistical calculations.

**Weakness:** The mean is sensitive to extreme values (**outliers**). A single very large or very small value can pull the mean away from the "typical" value in a misleading way.

<div class="callout example-box">
<span class="callout-title">Example</span>
**The outlier problem:** Five sales representatives have the following annual sales figures: \$420,000, \$385,000, \$402,000, \$398,000, \$1,850,000. The last rep had an exceptional year.

Mean = (\$420,000 + \$385,000 + \$402,000 + \$398,000 + \$1,850,000) / 5 = **\$691,000**

But four of the five reps have sales well below \$700,000. The mean is not representative of a "typical" rep. This is a case where the median is more informative.
</div>

### The Median

The **median** is the middle value in a data set when the values are arranged in order. It divides the data into two equal halves: 50% of values fall below the median and 50% fall above it.

**Finding the median:**
1. Sort the data from smallest to largest.
2. If $n$ is **odd**, the median is the value in position $\frac{n+1}{2}$.
3. If $n$ is **even**, the median is the average of the values in positions $\frac{n}{2}$ and $\frac{n}{2} + 1$.

**Example (odd $n$):** Seven daily call volumes: 43, 51, 29, 67, 55, 38, 71.
Sorted: 29, 38, 43, **51**, 55, 67, 71. Median = 51 (the 4th value out of 7).

**Example (even $n$):** Six transaction amounts: \$22, \$31, \$45, \$57, \$64, \$89.
Median = (45 + 57) / 2 = **\$51**.

**When to use the median:** The median is preferred when the data contains outliers or is skewed. It is the appropriate measure of center for **household income**, **home prices**, **salary distributions**, and other variables where extreme values are common. For ordinal data, the median is appropriate; the mean is not.

### The Mode

The **mode** is the value (or category) that appears most frequently in the data set.

- A data set can have **no mode** (all values appear once), **one mode** (unimodal), **two modes** (bimodal), or more.
- The mode is the only measure of central tendency that can be used for **nominal data**.

**Example:** A clothing store records the sizes purchased in one hour: S, M, L, M, XL, M, S, L, M. The mode is **M** (Medium), which appears 4 times. This tells the store which size to stock most heavily.

**When to use the mode:** Use the mode for categorical data, for identifying the most popular product or category, or whenever "the most frequent value" directly answers your business question.

## The Weighted Mean

When not all values carry equal importance, the **weighted mean** accounts for the relative weight (importance) of each value.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$\bar{x}_w = \frac{\sum_{i=1}^{n} w_i x_i}{\sum_{i=1}^{n} w_i}$$

where $w_i$ is the weight associated with value $x_i$.
</div>

**Example:** A student's final grade consists of: Homework (20%), Midterm Exam (35%), Final Exam (45%). Their scores are 88, 74, 91.

$$\bar{x}_w = \frac{(0.20)(88) + (0.35)(74) + (0.45)(91)}{0.20 + 0.35 + 0.45} = \frac{17.6 + 25.9 + 40.95}{1.00} = 84.45$$

Weighted average grade: **84.45**

A business use: computing a portfolio's average return when different assets have different weights based on investment amount.

## Measures of Variability

Two data sets can have the same mean but look completely different. Consider two customer wait times (in minutes):

- Store A: 5, 5, 5, 5, 5 (mean = 5 minutes)
- Store B: 1, 2, 5, 8, 9 (mean = 5 minutes)

The means are identical, but Store A has perfectly consistent wait times while Store B varies wildly. Measures of variability capture this spread.

### The Range

The **range** is the simplest measure of variability: the difference between the maximum and minimum values.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$\text{Range} = \text{Maximum} - \text{Minimum}$$
</div>

For Store B: Range = 9 – 1 = 8 minutes.

The range is quick to compute but uses only two data points and is highly sensitive to outliers.

### Variance and Standard Deviation

The **variance** and **standard deviation** are the most important measures of variability. They measure, on average, how far each data point deviates from the mean.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Sample variance:**
$$s^2 = \frac{\sum_{i=1}^{n}(x_i - \bar{x})^2}{n-1}$$

**Sample standard deviation:**
$$s = \sqrt{s^2} = \sqrt{\frac{\sum_{i=1}^{n}(x_i - \bar{x})^2}{n-1}}$$

**Population variance and standard deviation** use $N$ (population size) in the denominator instead of $n-1$: $\sigma^2 = \frac{\sum(x_i - \mu)^2}{N}$, $\sigma = \sqrt{\sigma^2}$.
</div>

Why $n-1$ instead of $n$ for the sample variance? Using $n-1$ (called **Bessel's correction**) makes the sample variance an unbiased estimator of the population variance. With only $n$ in the denominator, the sample variance would tend to underestimate the true population variance. You do not need to memorize this justification — just know that Excel's `=STDEV()` function uses $n-1$, which is what you want when working with sample data.

**Step-by-step example:**
Data set: 4, 7, 13, 2, 9 (sample of 5 daily return rates, %)

1. Mean: $\bar{x} = (4+7+13+2+9)/5 = 35/5 = 7$
2. Deviations from mean: $4-7=-3$, $7-7=0$, $13-7=6$, $2-7=-5$, $9-7=2$
3. Squared deviations: 9, 0, 36, 25, 4
4. Sum of squared deviations: $9+0+36+25+4 = 74$
5. Variance: $s^2 = 74/(5-1) = 74/4 = 18.5$
6. Standard deviation: $s = \sqrt{18.5} \approx 4.30\%$

The standard deviation of return rates is approximately 4.30%. This means a typical daily return deviates from the mean by about 4.30 percentage points.

### The Coefficient of Variation

The **coefficient of variation (CV)** expresses the standard deviation as a percentage of the mean, allowing comparisons of variability between data sets with different units or different means.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$CV = \frac{s}{\bar{x}} \times 100\%$$
</div>

**Example:** Two investment funds:
- Fund A: Mean annual return = 8%, Standard deviation = 2%, CV = 2/8 × 100% = **25%**
- Fund B: Mean annual return = 20%, Standard deviation = 9%, CV = 9/20 × 100% = **45%**

Fund B offers higher returns, but it is also considerably more volatile (45% CV vs. 25% CV). An investor who wants to maximize return per unit of risk would prefer Fund A.

## The Empirical Rule

For data that is approximately **bell-shaped (normally distributed)**, the **Empirical Rule** — sometimes called the 68-95-99.7 Rule — makes a powerful statement about where the data falls:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
For a bell-shaped distribution with mean $\mu$ and standard deviation $\sigma$:

- Approximately **68%** of the data falls within **1 standard deviation** of the mean: $(\mu - \sigma, \ \mu + \sigma)$
- Approximately **95%** of the data falls within **2 standard deviations** of the mean: $(\mu - 2\sigma, \ \mu + 2\sigma)$
- Approximately **99.7%** of the data falls within **3 standard deviations** of the mean: $(\mu - 3\sigma, \ \mu + 3\sigma)$
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Quality Control Application:** A bottling plant fills bottles with a mean fill volume of $\mu = 16.0$ oz and a standard deviation of $\sigma = 0.1$ oz. The fill volumes are approximately bell-shaped.

- 68% of bottles contain between 15.9 oz and 16.1 oz (within 1 SD)
- 95% of bottles contain between 15.8 oz and 16.2 oz (within 2 SD)
- 99.7% of bottles contain between 15.7 oz and 16.3 oz (within 3 SD)

A bottle filled to less than 15.7 oz or more than 16.3 oz would be extremely unusual — it falls outside three standard deviations. The quality control manager might flag such a bottle for inspection, as it likely indicates a process problem.
</div>

The Empirical Rule is only valid for approximately bell-shaped distributions. We will study the bell-shaped (normal) distribution in depth in Chapter 7.

## Percentiles and Quartiles

While the mean and median tell us about the center of a distribution, **percentiles** describe the complete picture of where values rank.

The **$k$th percentile** is the value below which $k\%$ of the data falls. (Note: there are slight variations in how percentiles are defined; we use the definition consistent with Excel's `=PERCENTILE.INC()` function.)

The most commonly used percentiles are the **quartiles**:
- **First Quartile ($Q_1$):** the 25th percentile. 25% of values fall below $Q_1$.
- **Second Quartile ($Q_2$):** the 50th percentile — the median. 50% of values fall below $Q_2$.
- **Third Quartile ($Q_3$):** the 75th percentile. 75% of values fall below $Q_3$.

The **Interquartile Range (IQR)** is the distance between the first and third quartile:

$$IQR = Q_3 - Q_1$$

The IQR captures the spread of the middle 50% of the data. It is resistant to outliers and is preferred over the range in many situations.

## The Five-Number Summary and Box Plots

The **five-number summary** condenses a data set into five key values:

$$\text{Minimum}, \quad Q_1, \quad \text{Median}\ (Q_2), \quad Q_3, \quad \text{Maximum}$$

These five numbers are displayed graphically in a **box plot** (also called a box-and-whisker plot):
- The **box** spans from $Q_1$ to $Q_3$ (the IQR)
- A line inside the box marks the **median**
- **Whiskers** extend from the box to the minimum and maximum (or to 1.5 × IQR beyond the quartiles, with outliers plotted separately)

Box plots are excellent for comparing distributions across groups and for quickly spotting skewness and outliers.

<div class="callout example-box">
<span class="callout-title">Example</span>
**Interpreting a Five-Number Summary:** A sample of 20 customer order values (\$) produces the following five-number summary:

- Minimum: \$12
- $Q_1$: \$38
- Median ($Q_2$): \$55
- $Q_3$: \$82
- Maximum: \$247

The IQR = \$82 – \$38 = \$44. The fact that the maximum (\$247) is far above $Q_3$ (\$82) suggests the data is right-skewed, with a few very large orders pulling the mean above the median. The range (\$235) is greatly inflated by this extreme order.
</div>

## Excel for Descriptive Statistics

Excel provides dedicated functions for every measure we have discussed.

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Key Excel Descriptive Statistics Functions:**

| What you want | Excel Function |
|---------------|---------------|
| Mean | `=AVERAGE(range)` |
| Median | `=MEDIAN(range)` |
| Mode | `=MODE.SNGL(range)` |
| Sample standard deviation | `=STDEV.S(range)` |
| Population standard deviation | `=STDEV.P(range)` |
| Sample variance | `=VAR.S(range)` |
| Population variance | `=VAR.P(range)` |
| Minimum | `=MIN(range)` |
| Maximum | `=MAX(range)` |
| $k$th percentile | `=PERCENTILE.INC(range, k)` where $k$ is between 0 and 1 |
| Quartiles | `=QUARTILE.INC(range, q)` where $q$ = 1, 2, or 3 |
| Count of values | `=COUNT(range)` |

**Example:** If your data is in cells A2:A51, the mean is `=AVERAGE(A2:A51)`, the median is `=MEDIAN(A2:A51)`, and the third quartile is `=QUARTILE.INC(A2:A51, 3)`.
</div>

### Using the Data Analysis ToolPak for Descriptive Statistics

Excel's **Data Analysis ToolPak** can produce a complete descriptive statistics summary in one step. This is the most efficient way to get a comprehensive overview of a data set.

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Step-by-Step: Descriptive Statistics with the Data Analysis ToolPak**

1. Enter your data in a single column (e.g., A1:A51, with "Sales Revenue" in A1 as a header).
2. Click the **Data** tab in the ribbon.
3. Click **Data Analysis** (in the Analysis group, far right).
4. Select **Descriptive Statistics** from the list and click **OK**.
5. In the dialog box:
   - **Input Range:** Select your data including the header (A1:A51).
   - Check **Labels in First Row** (since you included the header).
   - **Output Range:** Click a cell in an empty area of the sheet (e.g., C1) to place results there.
   - Check **Summary statistics**.
   - Optionally check **Kth Largest** and **Kth Smallest** for specific percentile values.
6. Click **OK**.

Excel will produce a table showing: Mean, Standard Error, Median, Mode, Standard Deviation, Sample Variance, Kurtosis, Skewness, Range, Minimum, Maximum, Sum, and Count.

**Note:** If you don't see "Data Analysis" under the Data tab, the ToolPak is not yet enabled. See the Preface for installation instructions.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Computing a Weighted Mean in Excel:** Use `=SUMPRODUCT()` to calculate a weighted mean efficiently.

If values are in column A (A2:A6) and weights are in column B (B2:B6), the weighted mean is:
`=SUMPRODUCT(A2:A6, B2:B6) / SUM(B2:B6)`

`SUMPRODUCT` multiplies corresponding values in two arrays and then sums the products — exactly the numerator of the weighted mean formula.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Mean</dt>
<dd>The arithmetic average of all values in a data set; sum of all values divided by number of values.</dd>

<dt>Median</dt>
<dd>The middle value in a sorted data set; the 50th percentile.</dd>

<dt>Mode</dt>
<dd>The most frequently occurring value in a data set.</dd>

<dt>Weighted Mean</dt>
<dd>An average that assigns different levels of importance (weights) to different values.</dd>

<dt>Range</dt>
<dd>The difference between the maximum and minimum values in a data set.</dd>

<dt>Variance ($s^2$)</dt>
<dd>The average of the squared deviations from the mean; the square of the standard deviation.</dd>

<dt>Standard Deviation ($s$)</dt>
<dd>The square root of the variance; measures the typical distance of data values from the mean, in the same units as the data.</dd>

<dt>Coefficient of Variation (CV)</dt>
<dd>The standard deviation expressed as a percentage of the mean; used to compare variability between data sets with different units or scales.</dd>

<dt>Empirical Rule</dt>
<dd>For bell-shaped distributions: approximately 68%, 95%, and 99.7% of data fall within 1, 2, and 3 standard deviations of the mean, respectively.</dd>

<dt>Percentile</dt>
<dd>The value below which a given percentage of observations fall.</dd>

<dt>Quartiles</dt>
<dd>The 25th ($Q_1$), 50th ($Q_2$), and 75th ($Q_3$) percentiles, dividing a data set into four equal parts.</dd>

<dt>Interquartile Range (IQR)</dt>
<dd>The difference $Q_3 - Q_1$; represents the spread of the middle 50% of the data.</dd>

<dt>Five-Number Summary</dt>
<dd>A compact description of a data set: Minimum, $Q_1$, Median, $Q_3$, Maximum.</dd>

<dt>Outlier</dt>
<dd>A data value that is far removed from the bulk of the data; often defined as a value more than 1.5 × IQR below $Q_1$ or above $Q_3$.</dd>
</dl>
</div>

---

## Exercises {-}

1. A regional bank branch records the number of new account openings per day for two weeks (10 business days): 12, 8, 15, 20, 9, 14, 18, 11, 16, 13.
   a. Calculate the **mean**, **median**, and **mode**.
   b. Calculate the **range**, **variance**, and **standard deviation** (show your work in a table with deviation and squared deviation columns).
   c. Enter this data in Excel and use `=AVERAGE()`, `=MEDIAN()`, `=STDEV.S()` to verify your answers.

2. A retail chain's seven stores reported the following weekly revenues (in thousands of dollars): \$182, \$215, \$197, \$643, \$188, \$201, \$193.
   a. Calculate the **mean** and **median**.
   b. Which measure better represents a "typical" store's revenue? Why?
   c. Remove the outlier (\$643) and recalculate the mean and median. How do they change? What does this illustrate about the sensitivity of the mean?

3. A university's career center records starting salaries for business graduates: \$42,000; \$48,000; \$55,000; \$52,000; \$61,000; \$47,000; \$58,000; \$44,000; \$53,000; \$49,000.
   a. Use Excel to compute the **five-number summary** (min, $Q_1$, median, $Q_3$, max).
   b. Compute the **IQR**. Are there any outliers using the rule: outlier if below $Q_1 - 1.5 \times IQR$ or above $Q_3 + 1.5 \times IQR$?
   c. Use the **Data Analysis ToolPak** to generate a full descriptive statistics report for this data.

4. A mutual fund's annual return rates over the past 10 years were: 8.2%, 11.5%, -3.4%, 14.7%, 6.1%, 9.8%, 2.3%, 12.0%, -1.5%, 7.9%.
   a. Compute the **mean** and **standard deviation** of annual returns.
   b. Apply the **Empirical Rule** to describe where approximately 68%, 95%, and 99.7% of annual returns would be expected to fall, assuming returns are approximately bell-shaped.
   c. One year the fund returned 18%. Is this unusual? Explain using the empirical rule.

5. A portfolio manager is comparing the performance of two investment strategies:
   - Strategy Alpha: Mean return = 9.5%, Standard deviation = 3.2%
   - Strategy Beta: Mean return = 14.8%, Standard deviation = 7.9%
   a. Calculate the **Coefficient of Variation** for each strategy.
   b. Which strategy has more variability relative to its return? Which would you recommend to a risk-averse investor? Explain.

6. A hotel loyalty program has three membership tiers: Basic (weight = 1), Silver (weight = 2), Gold (weight = 3). The average satisfaction score for each tier was: Basic = 72, Silver = 81, Gold = 88. There are 5,000 Basic, 2,000 Silver, and 1,000 Gold members.
   a. Calculate the **simple (unweighted) average** satisfaction score across tiers.
   b. Calculate the **weighted average** satisfaction score, using number of members as weights.
   c. Why are the two averages different? Which is more meaningful? Explain.

7. *Two call centers handle customer service inquiries. Call Center A has a mean handle time of 4.2 minutes with a standard deviation of 0.8 minutes. Call Center B has a mean handle time of 6.5 minutes with a standard deviation of 1.1 minutes. A supervisor says, "Call Center B is more variable." Do you agree? Support your answer with a specific calculation and explain your reasoning carefully.*

8. *A financial analyst examines quarterly earnings per share (EPS) for two companies over 12 quarters. Company X has mean EPS = \$2.40, standard deviation = \$0.95. Company Y has mean EPS = \$4.10, standard deviation = \$0.80. Using only this information, which company's earnings are more predictable? Which might be more attractive to a value investor who prizes stability? Justify your answers.*
