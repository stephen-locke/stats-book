# Correlation and Simple Linear Regression {#regression}

## Relationships Between Variables

A grocery chain notices that stores with more square footage tend to generate higher revenue. A real estate company finds that homes sell faster in neighborhoods with lower crime rates. A marketing team observes that weeks with higher advertising spending tend to be followed by stronger sales.

These are all examples of **relationships between variables** — patterns where knowing the value of one variable gives us information about the likely value of another. **Correlation** and **regression** are the statistical tools for studying, quantifying, and using these relationships.

In this chapter, we work with two quantitative variables and ask: Is there a relationship? How strong is it? Can we use one variable to predict the other? What business value can we extract from that prediction?

## Scatter Plots and Relationships

The first step in any regression analysis is always a **scatter plot** — a graph showing pairs of $(x, y)$ values as individual points. Before fitting any model, you must look at the data.

When examining a scatter plot, describe the relationship in terms of:

**Direction:**
- **Positive relationship:** As $x$ increases, $y$ tends to increase. (More advertising → more sales)
- **Negative relationship:** As $x$ increases, $y$ tends to decrease. (More price → fewer units sold)
- **No relationship:** Changes in $x$ are not associated with any consistent change in $y$.

**Strength:**
- **Strong:** Points cluster tightly along a line or curve.
- **Weak:** Points are loosely scattered with only a vague trend.
- **Moderate:** Somewhere in between.

**Form:**
- **Linear:** Points follow approximately a straight-line pattern.
- **Nonlinear/Curved:** Points follow a curve rather than a line. (Simple linear regression is appropriate only for linear relationships!)

**Outliers:** Individual points that fall far from the main pattern. Outliers can strongly affect correlation and regression results.

<div class="callout warning-box">
<span class="callout-title">Caution</span>
**Always plot your data before computing any statistics.** A scatter plot reveals the form (linear vs. curved), the presence of outliers, and whether the relationship is really consistent across the entire range of $x$. Fitting a straight line to curved data or data with severe outliers can produce a model that is technically computable but fundamentally misleading.
</div>

## Pearson Correlation Coefficient

The **Pearson correlation coefficient**, denoted $r$, measures the **strength and direction of the linear relationship** between two quantitative variables.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$r = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n}(x_i - \bar{x})^2 \cdot \sum_{i=1}^{n}(y_i - \bar{y})^2}}$$

This formula is always computed by software. The key properties to know:
</div>

**Properties of $r$:**
- $-1 \leq r \leq 1$ always.
- $r = +1$: perfect positive linear relationship (all points on an upward-sloping line)
- $r = -1$: perfect negative linear relationship (all points on a downward-sloping line)
- $r = 0$: no linear relationship (points show no linear trend)
- $r > 0$: positive direction; $r < 0$: negative direction
- $|r|$ close to 1: strong linear relationship; $|r|$ close to 0: weak linear relationship

**Guidelines for interpreting $|r|$** (these are rough conventions, not rigid rules):
- $|r| \geq 0.80$: strong linear relationship
- $0.50 \leq |r| < 0.80$: moderate linear relationship
- $0.30 \leq |r| < 0.50$: weak linear relationship
- $|r| < 0.30$: very weak or no linear relationship

<div class="callout warning-box">
<span class="callout-title">Caution</span>
**Correlation does not imply causation.** A high correlation between $x$ and $y$ means the two variables move together — it does not mean $x$ causes $y$. Ice cream sales and drowning rates are positively correlated (both are higher in summer), but eating ice cream does not cause drowning. In business, always think carefully about whether a causal mechanism makes sense before acting on a correlation.

Also, $r$ measures only **linear** relationships. Two variables can have a strong nonlinear relationship and still have $r \approx 0$ (for example, $y = x^2$ centered at $x=0$). Always examine the scatter plot.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Computing Correlation in Excel:**

`=CORREL(array1, array2)` — Computes the Pearson correlation coefficient $r$ between two arrays of data.

**Example:** If advertising spending is in A2:A13 and sales revenue is in B2:B13:
`=CORREL(A2:A13, B2:B13)` returns $r$.

**Correlation Matrix (multiple variables):** Use **Data → Data Analysis → Correlation**. Select all variable columns, check "Labels in First Row," and specify an output range. Excel produces a matrix of pairwise correlations — very useful for initial exploration of a multi-variable data set.
</div>

## Simple Linear Regression

**Simple linear regression** describes the linear relationship between one **predictor variable** (also called the independent variable or explanatory variable) $x$ and one **response variable** (dependent variable) $y$ using a straight-line equation.

### The Regression Equation

The true population regression model is:
$$y = \beta_0 + \beta_1 x + \varepsilon$$

where $\beta_0$ is the true intercept, $\beta_1$ is the true slope, and $\varepsilon$ is random error.

We estimate this model from sample data, producing the **estimated regression equation**:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$\hat{y} = b_0 + b_1 x$$

where:
- $\hat{y}$ ("y-hat") is the **predicted value** of $y$ for a given $x$
- $b_1$ is the **estimated slope** — the estimated change in $\hat{y}$ for a one-unit increase in $x$
- $b_0$ is the **estimated intercept** — the estimated value of $\hat{y}$ when $x = 0$
</div>

### The Least Squares Method

How do we find the "best" line? The **least squares method** finds the values of $b_0$ and $b_1$ that minimize the sum of the squared vertical distances (residuals) between the actual $y$ values and the predicted $\hat{y}$ values.

The **residual** for observation $i$ is: $e_i = y_i - \hat{y}_i$ (actual minus predicted).

Minimizing $\sum e_i^2 = \sum (y_i - \hat{y}_i)^2$ yields the formulas:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$b_1 = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{\sum_{i=1}^{n}(x_i - \bar{x})^2} = r \cdot \frac{s_y}{s_x}$$

$$b_0 = \bar{y} - b_1 \bar{x}$$

The regression line always passes through the point $(\bar{x}, \bar{y})$.
</div>

Conceptually: the numerator of $b_1$ measures how $x$ and $y$ co-vary; the denominator measures how much $x$ alone varies. The slope is the ratio of their joint variation to $x$'s individual variation.

## Interpreting the Slope and Intercept

The **slope** $b_1$ has a specific, actionable business interpretation:

"For each additional one unit in $x$, the predicted value of $y$ changes by $b_1$ units, holding all else constant."

The **intercept** $b_0$ is the predicted value of $y$ when $x = 0$. The intercept often has a meaningful interpretation, but sometimes $x = 0$ falls outside the range of the data, in which case the intercept should not be interpreted literally.

<div class="callout example-box">
<span class="callout-title">Example</span>
**Advertising and Sales**

A company collects monthly data on advertising spending ($x$, in thousands of dollars) and sales revenue ($y$, in thousands of dollars) for 12 months. A regression analysis produces:

$$\hat{y} = 42.5 + 8.3x$$

**Interpreting the slope:** For each additional \$1,000 spent on advertising, predicted monthly sales revenue increases by \$8,300. The return is \$8.30 in sales for every \$1 spent on advertising.

**Interpreting the intercept:** When advertising spending is \$0, predicted monthly sales revenue is \$42,500. This might represent baseline sales from customer loyalty, repeat purchases, and word-of-mouth — sales that occur even without advertising.

**Prediction:** If the company plans to spend \$20,000 on advertising next month ($x = 20$):
$\hat{y} = 42.5 + 8.3(20) = 42.5 + 166 = \$208,500$

Predicted sales revenue: **\$208,500**
</div>

## The Coefficient of Determination ($R^2$)

The **coefficient of determination**, $R^2$ (also written $r^2$), measures the **proportion of the total variation in $y$ that is explained by the regression model** (i.e., explained by $x$).

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$R^2 = r^2 \qquad \text{(for simple linear regression, } R^2 \text{ is literally the square of } r\text{)}$$

Equivalently:
$$R^2 = \frac{SSR}{SST} = 1 - \frac{SSE}{SST}$$

where:
- $SST = \sum(y_i - \bar{y})^2$ = Total Sum of Squares (total variation in $y$)
- $SSR = \sum(\hat{y}_i - \bar{y})^2$ = Regression Sum of Squares (variation explained by the model)
- $SSE = \sum(y_i - \hat{y}_i)^2 = \sum e_i^2$ = Error Sum of Squares (unexplained variation)
</div>

**Interpreting $R^2$:**
- $R^2 = 0.85$ means the model explains 85% of the variation in $y$. The remaining 15% is due to factors not captured by $x$ (measurement error, other variables, random chance).
- $R^2 = 1.0$: perfect fit — all points lie exactly on the regression line (rare and suspicious in real data).
- $R^2 = 0$: the model explains nothing — $x$ tells us nothing useful about $y$.

**Business context:** In social science and business data, $R^2$ values of 0.50 to 0.80 are common for well-specified models. Very high $R^2$ (>0.95) often occurs with time trends but may reflect spurious relationships.

## Residuals and Checking Model Fit

The **residuals** $e_i = y_i - \hat{y}_i$ are the "leftovers" after fitting the regression line — the part of each $y$ value not explained by the model.

Examining residuals helps assess whether the regression model is appropriate:

**Residual plot:** Plot residuals ($y$-axis) versus predicted values or $x$ values ($x$-axis). A good residual plot shows:
- Points scattered randomly around zero (no pattern)
- Roughly constant vertical spread across all values of $x$ (homoscedasticity)

**Warning signs in residual plots:**
- **A curve or arc:** indicates the true relationship is nonlinear — a straight line is the wrong model.
- **A funnel shape (increasing spread):** indicates non-constant variance (heteroscedasticity) — predictions become less reliable as $x$ increases.
- **Obvious outliers:** single points far from the rest may disproportionately influence the regression line.

## Making Predictions and Understanding Their Limits

Once you have the regression equation, you can use it for prediction. But prediction comes with important limitations:

**Interpolation vs. extrapolation:** A prediction for an $x$ value within the range of the original data (**interpolation**) is generally reliable, assuming the model is good. A prediction for an $x$ value far outside the range (**extrapolation**) may be wildly inaccurate — the linear relationship may not hold outside the observed range.

<div class="callout warning-box">
<span class="callout-title">Caution</span>
**Never extrapolate beyond the range of your data without strong justification.** If your regression of sales on advertising was estimated using months with advertising spending between \$5,000 and \$50,000, do not use the equation to predict sales for a \$500,000 advertising month. The relationship might change dramatically at that scale.
</div>

## Excel for Regression Analysis

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Individual Regression Functions in Excel:**

- `=SLOPE(y_range, x_range)` — computes $b_1$
- `=INTERCEPT(y_range, x_range)` — computes $b_0$
- `=RSQ(y_range, x_range)` — computes $R^2$
- `=CORREL(x_range, y_range)` — computes $r$

**Example** (advertising in A2:A13, sales in B2:B13):
```
=SLOPE(B2:B13, A2:A13)          → b1 = 8.30
=INTERCEPT(B2:B13, A2:A13)      → b0 = 42.50
=RSQ(B2:B13, A2:A13)            → R-squared = 0.87
```

**LINEST Function** (returns multiple regression statistics at once):
`=LINEST(y_range, x_range, TRUE, TRUE)` entered as an **array formula** (Ctrl+Shift+Enter in older Excel; just Enter in Excel 365) returns a 5×2 array containing slope, intercept, standard errors, $R^2$, F-statistic, and more.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Full Regression Output Using the Data Analysis ToolPak:**

This is the most complete and practical approach for business analysis:

1. Go to **Data → Data Analysis → Regression → OK**.
2. **Input Y Range:** Select your response variable column (including header).
3. **Input X Range:** Select your predictor variable column (including header).
4. Check **Labels**.
5. Check **Residuals** and **Residual Plots** to get residual diagnostics.
6. Check **Line Fit Plots** to see the fitted line overlaid on the data.
7. Set **Output Range** to a blank area of the sheet and click **OK**.

The output includes:
- **Regression Statistics:** $R$, $R^2$, Adjusted $R^2$, Standard Error, number of observations
- **ANOVA table:** SSR, SSE, SST, F-statistic, p-value for the overall model
- **Coefficients table:** $b_0$, $b_1$, standard errors, t-statistics, p-values, and 95% confidence intervals for each coefficient

The **p-value for $b_1$** tests $H_0: \beta_1 = 0$ (no linear relationship). If this p-value < $\alpha$, the linear relationship is statistically significant.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Adding a Trendline to a Scatter Plot in Excel:**

1. Create a scatter plot (Insert → Scatter).
2. Click on any data point to select the series.
3. Right-click and select **Add Trendline**.
4. Choose **Linear**.
5. Check **Display Equation on chart** and **Display R-squared value on chart**.

The equation displayed is the regression equation. **Note:** The trendline equation and $R^2$ shown on the chart are identical to what you'd compute with `=SLOPE`, `=INTERCEPT`, and `=RSQ`.
</div>

<div class="callout example-box">
<span class="callout-title">Example</span>
**Reading Regression Output from the ToolPak**

A ToolPak regression of Sales ($y$) on Advertising ($x$) returns (abbreviated):

```
R Square:  0.872
Standard Error: 12.4

Coefficients  Std Error   t Stat   P-value   Lower 95%  Upper 95%
Intercept  42.5   8.3    5.12   0.0004    24.4       60.6
Advertising 8.30  0.79   10.51  0.0000     6.59        9.99
```

**Reading the output:**
- $R^2 = 0.872$: 87.2% of variation in sales is explained by advertising spending.
- Standard error of the regression = 12.4 thousand dollars: typical prediction error.
- Intercept = 42.5, Slope = 8.3: the regression equation is $\hat{y} = 42.5 + 8.3x$.
- p-value for slope = 0.000: the slope is highly significant ($p < 0.001$); advertising spending is a statistically significant predictor of sales.
- 95% CI for slope: (6.59, 9.99) — we are 95% confident the true slope is between 6.59 and 9.99.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Correlation</dt>
<dd>A measure of the strength and direction of the linear relationship between two quantitative variables.</dd>

<dt>Pearson Correlation Coefficient ($r$)</dt>
<dd>A dimensionless number between -1 and +1 measuring the strength and direction of the linear association between $x$ and $y$.</dd>

<dt>Simple Linear Regression</dt>
<dd>A model describing the linear relationship between a predictor variable $x$ and a response variable $y$, yielding the equation $\hat{y} = b_0 + b_1 x$.</dd>

<dt>Predictor Variable ($x$)</dt>
<dd>The independent or explanatory variable used to predict $y$ in a regression model.</dd>

<dt>Response Variable ($y$)</dt>
<dd>The dependent variable being predicted or explained in a regression model.</dd>

<dt>Slope ($b_1$)</dt>
<dd>The estimated change in $\hat{y}$ for each one-unit increase in $x$; the steepness and direction of the regression line.</dd>

<dt>Intercept ($b_0$)</dt>
<dd>The estimated value of $\hat{y}$ when $x = 0$; where the regression line crosses the $y$-axis.</dd>

<dt>Least Squares Method</dt>
<dd>The method for finding the regression line that minimizes the sum of squared residuals $\sum(y_i - \hat{y}_i)^2$.</dd>

<dt>Residual ($e_i$)</dt>
<dd>The difference between an observed $y$ value and its predicted value from the regression: $e_i = y_i - \hat{y}_i$.</dd>

<dt>Coefficient of Determination ($R^2$)</dt>
<dd>The proportion of total variation in $y$ explained by the regression model; ranges from 0 to 1.</dd>

<dt>Extrapolation</dt>
<dd>Predicting $y$ for an $x$ value outside the range of the data used to fit the regression; generally unreliable.</dd>

<dt>Residual Plot</dt>
<dd>A scatter plot of residuals vs. fitted values or $x$; used to check for model adequacy (linearity, constant variance, no patterns).</dd>
</dl>
</div>

---

## Exercises {-}

1. A real estate analyst collects data on 10 properties, recording the size of each home (square feet, $x$) and its sale price (\$000, $y$):

   | Size ($x$) | 1,200 | 1,500 | 1,800 | 2,100 | 2,400 | 1,650 | 2,250 | 1,950 | 1,400 | 2,700 |
   |-----------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|
   | Price ($y$) | 215 | 278 | 310 | 382 | 450 | 289 | 405 | 345 | 242 | 498 |

   a. Create a **scatter plot** in Excel. Describe the direction, strength, and form of the relationship.
   b. Compute the **correlation coefficient** $r$ using `=CORREL`. Interpret the value.
   c. Use `=SLOPE` and `=INTERCEPT` to find the regression equation.
   d. Interpret the **slope** in the context of real estate.
   e. Predict the sale price of a 2,000 square foot home.

2. A grocery store manager is investigating the relationship between shelf space (in feet, $x$) allocated to a snack product and its weekly sales (units, $y$). Using 8 weeks of data, she computes: $\bar{x} = 6.5$ feet, $\bar{y} = 148$ units, $b_1 = 22.4$ units/foot.
   a. Find the regression equation.
   b. Interpret the slope in context.
   c. Predict weekly sales if 8 feet of shelf space is allocated.
   d. If $r = 0.88$, compute $R^2$ and interpret it.

3. A marketing analyst runs a regression of monthly website sales revenue ($y$, in \$000) on monthly email campaigns sent ($x$). The Data Analysis ToolPak produces these coefficients:

   - Intercept: 34.2 (p-value = 0.0120)
   - Slope (email campaigns): 4.8 (p-value = 0.0003)
   - $R^2 = 0.712$

   a. Write the regression equation.
   b. Is the slope statistically significant at $\alpha = 0.05$? How do you know?
   c. Interpret $R^2 = 0.712$ in plain language.
   d. Predict revenue if 10 email campaigns are sent in a month.
   e. Should the analyst conclude that sending more emails *causes* higher revenue? Why or why not?

4. Using the data from Exercise 1, run the full **Data Analysis ToolPak Regression** in Excel. Report:
   a. The $R^2$ value and standard error of the regression.
   b. The t-statistic and p-value for the slope. Is the relationship statistically significant at $\alpha = 0.01$?
   c. The 95% confidence interval for the slope. Interpret it in context.
   d. Create and examine the **residual plot**. Does it show any concerning patterns?

5. An HR analyst is studying whether employee tenure ($x$, years) predicts annual performance review scores ($y$, out of 100). For 15 employees: $\bar{x} = 4.2$ years, $\bar{y} = 72.4$ points, $\sum(x_i - \bar{x})^2 = 48.6$, $\sum(x_i - \bar{x})(y_i - \bar{y}) = 31.5$, $SST = 840$, $SSE = 617$.
   a. Compute $b_1$, $b_0$, and the regression equation.
   b. Compute $SSR$ and $R^2$. Interpret $R^2$.
   c. Is tenure a strong predictor of performance scores? What other variables might the analyst add to improve the model?

6. A sales manager records the number of client visits ($x$) and monthly sales (in \$000, $y$) for 12 salespeople: the summary statistics are $n=12$, $\sum x = 144$, $\sum y = 1,728$, $\sum x^2 = 1,896$, $\sum y^2 = 261,360$, $\sum xy = 22,320$.
   a. Compute $\bar{x}$ and $\bar{y}$.
   b. Compute $b_1$ and $b_0$.
   c. Compute $r$ using the formula $r = \frac{n\sum xy - \sum x \sum y}{\sqrt{[n\sum x^2 - (\sum x)^2][n\sum y^2 - (\sum y)^2]}}$.
   d. Interpret the correlation and regression results for the sales manager.

7. *A company's analyst fits a regression of annual revenue ($y$, millions) on the number of sales representatives employed ($x$). The equation is $\hat{y} = 12.4 + 0.85x$ with $R^2 = 0.71$. The data ranges from 15 to 60 sales reps. Critically evaluate the following uses of this model:*
   - *Predicting revenue for 35 sales reps*
   - *Predicting revenue for 150 sales reps*
   - *Concluding that hiring more reps will increase revenue*
   - *Using the equation to set sales rep headcount targets for next year*

8. *Research and describe a real-world business application where **spurious correlation** might arise — two variables that are strongly correlated but where no causal relationship exists. Explain what "lurking variable" might explain the observed correlation.*
