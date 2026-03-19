# Chi-Square Tests {#chi-square}

## When the Data Is Categorical

All of the hypothesis tests in Chapters 10 and 11 dealt with numerical variables — we were testing claims about means or proportions. But many important business questions involve categorical data:

- Do customers in different age groups prefer different product sizes?
- Is a die fair (i.e., do all six faces appear equally often)?
- Are customer satisfaction ratings distributed the way the company's model predicts?
- Is there an association between an employee's department and their level of engagement?

These questions cannot be answered with t-tests or Z-tests, because the data does not consist of numerical measurements. Instead, we use the **chi-square ($\chi^2$) test**, a family of tests designed for categorical data.

In this chapter, we study two forms of the chi-square test:
1. **Goodness-of-fit test:** Does the observed distribution of a single categorical variable match a hypothesized distribution?
2. **Test of independence:** Are two categorical variables independent of each other?

## The Chi-Square Statistic

Both tests use the same fundamental statistic: the chi-square test statistic compares **observed frequencies** (what we actually counted in the data) to **expected frequencies** (what we would expect to see if the null hypothesis were true).

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Chi-square test statistic:**
$$\chi^2 = \sum_{\text{all cells}} \frac{(O - E)^2}{E}$$

where:
- $O$ = observed frequency in a cell
- $E$ = expected frequency in a cell (assuming $H_0$ is true)

A larger $\chi^2$ means the observed data deviates more from what $H_0$ predicts — stronger evidence against $H_0$.
</div>

The chi-square distribution is right-skewed and takes only non-negative values. The rejection region is always in the right tail (large values of $\chi^2$ indicate the observed data is far from expected).

## The Chi-Square Goodness-of-Fit Test

### Concept

The **goodness-of-fit test** tests whether the distribution of a single categorical variable in the population matches a **specific hypothesized distribution**.

$H_0$: The population distribution matches the hypothesized distribution.
$H_a$: The population distribution does not match the hypothesized distribution.

### Computing Expected Frequencies

For the goodness-of-fit test, the expected frequency for each category is:
$$E_i = n \times p_{0i}$$
where $n$ is the total sample size and $p_{0i}$ is the hypothesized probability for category $i$.

### Degrees of Freedom

$$df = k - 1$$
where $k$ is the number of categories.

### Conditions

- Each expected frequency must be at least **5**: $E_i \geq 5$ for all $i$.
- The observations must be independent.

<div class="callout example-box">
<span class="callout-title">Example</span>
**Goodness-of-Fit: Market Share Analysis**

A snack food company believes its four brands hold equal market share (25% each). A market research firm surveys 400 consumers and records their preferred brand:

| Brand | Observed ($O$) | Expected ($E = 400 \times 0.25$) | $(O-E)^2/E$ |
|-------|--------------|-------------------------------|------------|
| Alpha | 115 | 100 | $(115-100)^2/100 = 2.25$ |
| Beta | 92 | 100 | $(92-100)^2/100 = 0.64$ |
| Gamma | 108 | 100 | $(108-100)^2/100 = 0.64$ |
| Delta | 85 | 100 | $(85-100)^2/100 = 2.25$ |
| **Total** | **400** | **400** | $\chi^2 = \mathbf{5.78}$ |

$H_0$: All four brands have equal 25% market share.
$H_a$: The market shares are not all equal.

$df = 4 - 1 = 3$, $\alpha = 0.05$

**Critical value:** `=CHISQ.INV.RT(0.05, 3)` → 7.815

**P-value:** `=CHISQ.DIST.RT(5.78, 3)` → 0.123

Since $\chi^2 = 5.78 < 7.815$ (critical value), and p-value $= 0.123 > 0.05 = \alpha$, **fail to reject $H_0$**.

**Conclusion:** There is insufficient evidence at the 5% level to conclude that the market shares differ from the hypothesized 25% each. The observed variation is consistent with random sampling variability.
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Goodness-of-Fit with Unequal Hypothesized Proportions**

A retailer's historical sales records show that purchases by day of week follow this pattern: Monday 10%, Tuesday 12%, Wednesday 14%, Thursday 15%, Friday 22%, Saturday 19%, Sunday 8%. This past week, total transactions were 500, with the following counts by day:

| Day | $O$ | Expected $p$ | $E = 500p$ | $(O-E)^2/E$ |
|-----|-----|-------------|----------|------------|
| Mon | 56 | 0.10 | 50 | 0.72 |
| Tue | 63 | 0.12 | 60 | 0.15 |
| Wed | 68 | 0.14 | 70 | 0.06 |
| Thu | 74 | 0.15 | 75 | 0.01 |
| Fri | 108 | 0.22 | 110 | 0.04 |
| Sat | 101 | 0.19 | 95 | 0.38 |
| Sun | 30 | 0.08 | 40 | 2.50 |
| **Total** | **500** | **1.00** | **500** | $\chi^2 = \mathbf{3.86}$ |

$df = 7 - 1 = 6$. p-value = `=CHISQ.DIST.RT(3.86, 6)` → 0.695.

Since p-value (0.695) >> 0.05, **fail to reject $H_0$**. This week's sales pattern is consistent with the historical pattern.
</div>

## The Chi-Square Test of Independence

### Concept

The **test of independence** tests whether two categorical variables are **independent** (unrelated) in the population.

$H_0$: The two variables are independent.
$H_a$: The two variables are not independent (they are associated).

Data is arranged in a **contingency table** (cross-tabulation) with $r$ rows and $c$ columns.

### Computing Expected Frequencies

Under $H_0$ (independence), the expected frequency for each cell is:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$E_{ij} = \frac{(\text{Row } i \text{ total}) \times (\text{Column } j \text{ total})}{\text{Grand total}}$$

**Degrees of freedom:**
$$df = (r-1)(c-1)$$

where $r$ = number of rows and $c$ = number of columns (not counting totals).
</div>

### Conditions

- The data is from a random sample.
- All expected cell frequencies are at least 5: $E_{ij} \geq 5$ for all cells. If some expected frequencies are below 5, consider combining categories.

<div class="callout example-box">
<span class="callout-title">Example</span>
**Test of Independence: Customer Satisfaction and Purchase Channel**

A retailer surveys 600 customers, recording their preferred shopping channel (Online, In-Store, Phone) and satisfaction level (Satisfied, Neutral, Dissatisfied). They want to know whether satisfaction is independent of shopping channel.

**Observed frequencies:**

| | Online | In-Store | Phone | **Row Total** |
|-|--------|----------|-------|-------------|
| Satisfied | 160 | 190 | 80 | **430** |
| Neutral | 50 | 60 | 30 | **140** |
| Dissatisfied | 20 | 30 | 10 | **60** |
| **Col Total** | **230** | **280** | **120** | **600** |

**Expected frequencies** (using $E_{ij} = \text{Row total} \times \text{Col total} / 600$):

| | Online | In-Store | Phone |
|-|--------|----------|-------|
| Satisfied | $430 \times 230/600 = 164.83$ | $430 \times 280/600 = 200.67$ | $430 \times 120/600 = 86.00$ |
| Neutral | $140 \times 230/600 = 53.67$ | $140 \times 280/600 = 65.33$ | $140 \times 120/600 = 28.00$ |
| Dissatisfied | $60 \times 230/600 = 23.00$ | $60 \times 280/600 = 28.00$ | $60 \times 120/600 = 12.00$ |

All expected frequencies exceed 5. ✓

**Chi-square calculation:**

$$\chi^2 = \frac{(160-164.83)^2}{164.83} + \frac{(190-200.67)^2}{200.67} + \frac{(80-86)^2}{86} + \cdots$$

Computing all 9 terms: $\chi^2 \approx 0.142 + 0.568 + 0.419 + 0.250 + 0.436 + 0.143 + 0.391 + 0.143 + 0.333 = 2.825$

$df = (3-1)(3-1) = 4$

**P-value:** `=CHISQ.DIST.RT(2.825, 4)` → 0.587

Since p-value (0.587) >> 0.05, **fail to reject $H_0$**.

**Conclusion:** There is no statistically significant evidence that customer satisfaction and shopping channel are related. Satisfaction appears to be independent of channel.
</div>

## Excel for Chi-Square Tests

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Chi-Square Functions in Excel:**

`=CHISQ.DIST.RT(x, deg_freedom)` — Right-tail p-value: $P(\chi^2 > x)$

`=CHISQ.INV.RT(probability, deg_freedom)` — Critical value: the $\chi^2$ value with `probability` in the right tail

`=CHISQ.TEST(actual_range, expected_range)` — Returns the p-value of the chi-square test directly, given ranges of observed and expected frequencies

**Key formulas for the functions:**
- p-value from test statistic: `=CHISQ.DIST.RT(chi_sq_stat, df)`
- Critical value at $\alpha = 0.05$: `=CHISQ.INV.RT(0.05, df)`
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Step-by-Step Chi-Square Test of Independence in Excel:**

**Step 1: Enter the observed frequencies** in a table (e.g., rows 2–4, columns B–D for a 3×3 table). Add row totals in column E and column totals in row 5.

**Step 2: Compute expected frequencies** in a separate table (e.g., starting in row 8). For cell B8 (expected for row 1, col 1):
`=E$2*B$5/E$5` — uses mixed references to pick up the correct row total (E2, rows locked), column total (B5, columns locked), and grand total (E5, both locked). Copy this formula to all expected frequency cells.

**Step 3: Compute chi-square contributions** in another table:
`=(B2-B8)^2/B8` — observed cell minus expected cell, squared, divided by expected. Copy to all cells.

**Step 4: Sum the chi-square contributions:**
`=SUM(chi-sq-contribution-range)` → this is your $\chi^2$ statistic.

**Step 5: Compute df and p-value:**
```
df = (rows-1)*(cols-1)
p-value = =CHISQ.DIST.RT(chi_sq_stat, df)
```

**Shortcut using CHISQ.TEST:**
`=CHISQ.TEST(observed_range, expected_range)` — returns the p-value directly.
This is the fastest approach once you have computed the expected frequencies.
</div>

## Business Applications

### Market Research

Chi-square tests of independence are standard tools in market research:
- "Do customers in different income brackets prefer different product tiers?"
- "Is there a relationship between a customer's age group and their primary social media platform?"
- "Does customer loyalty status affect which promotion type they respond to?"

### Customer Satisfaction Analysis

Goodness-of-fit tests can check whether satisfaction score distributions have shifted over time:
- "Does this quarter's satisfaction distribution match last quarter's distribution?"
- "Does our satisfaction distribution match the industry benchmark distribution?"

### Quality Control

- "Is the distribution of defect types this month consistent with the expected distribution from process engineering?"
- "Do defect rates differ across production shifts?" (Test of independence: shift vs. defect status)

### Human Resources

- "Is there a relationship between employees' educational background and their career advancement tier?"
- "Do training participation rates differ across departments?" (Test of independence: department vs. participation)

<div class="callout note-box">
<span class="callout-title">Note</span>
A statistically significant chi-square test tells you that the variables are associated — but it does not tell you the nature or strength of the association. Follow up a significant test by examining the observed vs. expected frequencies to identify which cells show the biggest discrepancies (largest $(O-E)^2/E$ values). These are the cells where the observed pattern most deviates from independence, and they reveal the business story behind the result.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Chi-Square Test Statistic ($\chi^2$)</dt>
<dd>A measure of the total discrepancy between observed and expected frequencies: $\chi^2 = \sum(O-E)^2/E$. Follows a chi-square distribution under $H_0$.</dd>

<dt>Chi-Square Distribution</dt>
<dd>A family of right-skewed, non-negative distributions defined by degrees of freedom; the distribution of $\chi^2$ under the null hypothesis.</dd>

<dt>Observed Frequency ($O$)</dt>
<dd>The actual count of observations in a category or cell, obtained from the sample data.</dd>

<dt>Expected Frequency ($E$)</dt>
<dd>The count expected in a category or cell if the null hypothesis were true; computed from row/column totals or hypothesized proportions.</dd>

<dt>Goodness-of-Fit Test</dt>
<dd>A chi-square test that compares the observed distribution of a single categorical variable to a hypothesized distribution.</dd>

<dt>Test of Independence</dt>
<dd>A chi-square test that determines whether two categorical variables are independent (unrelated) in the population, using data arranged in a contingency table.</dd>

<dt>Degrees of Freedom (Chi-Square)</dt>
<dd>For goodness-of-fit: $df = k - 1$ (number of categories minus one). For test of independence: $df = (r-1)(c-1)$.</dd>

<dt>Contingency Table</dt>
<dd>A cross-tabulation table showing the joint frequency distribution of two categorical variables; the input for the chi-square test of independence.</dd>
</dl>
</div>

---

## Exercises {-}

1. A financial advisor believes that her clients' investment preference follows this distribution: Stocks 50%, Bonds 30%, Real Estate 15%, Other 5%. She surveys a random sample of 200 clients and finds: Stocks 95, Bonds 65, Real Estate 28, Other 12.
   a. State $H_0$ and $H_a$.
   b. Compute the expected frequencies for each category.
   c. Check the condition that all expected frequencies are at least 5.
   d. Compute the $\chi^2$ test statistic.
   e. Find the p-value and state your conclusion at $\alpha = 0.10$.

2. A company's HR department classifies employee absences into four categories: Illness, Personal, Family, and Other. Company policy assumes the distribution is: 45% Illness, 25% Personal, 20% Family, 10% Other. A random sample of 400 absence records from last year shows: Illness 168, Personal 112, Family 78, Other 42.
   a. At $\alpha = 0.05$, is there sufficient evidence that the actual absence distribution differs from policy assumptions?
   b. Use Excel's `CHISQ.DIST.RT` to find the exact p-value.
   c. Which categories show the greatest deviations from expected? What might explain those deviations?

3. A grocery chain surveys 450 customers about their **household income bracket** (Low, Middle, High) and **preferred store format** (Discount, Standard, Premium). The observed data is:

   | | Discount | Standard | Premium | **Total** |
   |-|----------|----------|---------|---------|
   | **Low income** | 90 | 55 | 15 | **160** |
   | **Middle income** | 60 | 95 | 45 | **200** |
   | **High income** | 20 | 50 | 20 | **90** |
   | **Total** | **170** | **200** | **80** | **450** |

   a. State the null and alternative hypotheses.
   b. Compute all expected frequencies in Excel (use the `=Row_Total*Col_Total/Grand_Total` formula).
   c. Check whether all expected frequencies are at least 5.
   d. Compute the $\chi^2$ statistic and degrees of freedom.
   e. Use `=CHISQ.DIST.RT` to find the p-value. At $\alpha = 0.01$, state your conclusion.
   f. If you reject $H_0$, describe which income-format combinations show the most deviation from independence.

4. A quality manager at a production facility tracks defect types across three production shifts. The observed counts are:

   | | Surface Defect | Dimensional Defect | Assembly Defect | **Total** |
   |-|---------------|-------------------|----------------|---------|
   | **Day Shift** | 22 | 15 | 8 | **45** |
   | **Evening Shift** | 18 | 22 | 10 | **50** |
   | **Night Shift** | 30 | 18 | 7 | **55** |
   | **Total** | **70** | **55** | **25** | **150** |

   a. Is there evidence at $\alpha = 0.05$ that defect type and shift are associated?
   b. Use the Excel `CHISQ.TEST` function to compute the p-value directly, given that you have already set up the observed and expected frequency tables.
   c. What practical actions might the quality manager take based on the results?

5. An e-commerce company tracks customer purchase completion rates across four website designs (A, B, C, D). Each design was shown to 250 customers:

   | Design | Purchased | Did Not Purchase |
   |--------|-----------|-----------------|
   | A | 42 | 208 |
   | B | 58 | 192 |
   | C | 51 | 199 |
   | D | 67 | 183 |

   a. Test whether purchase completion rate is independent of website design at $\alpha = 0.05$.
   b. Based on the observed data, which design has the highest conversion rate? Does the chi-square test tell you which specific designs differ from each other?

6. *A marketing team hypothesizes that customer age (Under 30 / 30–50 / Over 50) and preferred communication channel (Email / Text / Phone / Social Media) are independent. A survey of 800 customers produces the following results:*

   | | Email | Text | Phone | Social Media | **Total** |
   |-|-------|------|-------|-------------|---------|
   | **Under 30** | 55 | 95 | 20 | 80 | **250** |
   | **30–50** | 120 | 60 | 55 | 65 | **300** |
   | **Over 50** | 110 | 30 | 85 | 25 | **250** |
   | **Total** | **285** | **185** | **160** | **170** | **800** |

   *a. Conduct the full chi-square test of independence in Excel (compute expected frequencies, chi-square statistic, degrees of freedom, and p-value). Use $\alpha = 0.01$.*
   *b. State your conclusion and explain its marketing implications: if the variables are associated, how should the marketing team adjust its communication strategy?*
