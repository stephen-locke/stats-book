# Data Visualization {#visualization}

## A Picture Is Worth a Thousand Numbers

A spreadsheet full of numbers is hard to absorb. A well-constructed chart makes patterns immediately visible — the seasonal spike in holiday sales, the steady upward trend in website traffic, the department whose cost variance is wildly out of line with the others. Data visualization translates numbers into pictures that support faster, better decision-making.

In this chapter, we build the toolkit of standard business charts, learn how to construct them in Excel, and — just as importantly — learn when each type of chart is and is not appropriate. We also introduce **frequency distributions**, which underlie several chart types and form a bridge between raw data and graphical summary.

## Frequency Distributions

Before we can draw a histogram or discuss a bar chart meaningfully, we need to understand how to organize data into a **frequency distribution** — a table that shows how often each value (or range of values) occurs.

### Frequency Distributions for Categorical Data

For qualitative data, simply count how many observations fall into each category.

<div class="callout example-box">
<span class="callout-title">Example</span>
A clothing store records the payment method for 200 transactions:

| Payment Method | Frequency | Relative Frequency |
|---------------|-----------|-------------------|
| Credit Card | 102 | 102/200 = 51.0% |
| Debit Card | 54 | 54/200 = 27.0% |
| Mobile Payment | 28 | 28/200 = 14.0% |
| Cash | 16 | 16/200 = 8.0% |
| **Total** | **200** | **100.0%** |

The **relative frequency** of a category is its frequency divided by the total number of observations: $\text{Relative Frequency} = f / n$.
</div>

### Frequency Distributions for Quantitative Data

For numerical data, we group values into **classes** (also called bins or intervals) and count how many observations fall in each class.

**Rules for constructing a frequency distribution for quantitative data:**

1. Use between **5 and 20 classes** — enough to show the shape of the distribution, but not so many that the pattern is lost.
2. Make all classes the same **width** (when possible).
3. Classes should be **mutually exclusive** (no overlap) and **exhaustive** (every value fits in exactly one class).

**Class width formula:**
$$\text{Class width} \approx \frac{\text{Maximum} - \text{Minimum}}{\text{Number of classes}}$$
Round up to a convenient number.

<div class="callout example-box">
<span class="callout-title">Example</span>
Customer wait times (in minutes) for 30 service calls: 2.1, 4.7, 1.8, 6.3, 3.5, 8.1, 5.2, 2.9, 7.4, 3.1, 4.0, 5.8, 6.7, 1.5, 9.2, 4.4, 3.8, 7.0, 2.6, 5.5, 8.8, 3.3, 6.1, 4.9, 2.2, 7.6, 5.0, 1.9, 8.5, 4.2.

Min = 1.5, Max = 9.2. Using 5 classes: width ≈ (9.2 − 1.5)/5 = 1.54, round up to 2.

| Class (minutes) | Frequency | Relative Frequency | Cumulative Freq. |
|----------------|-----------|-------------------|-----------------|
| 1.5 – < 3.5 | 7 | 23.3% | 23.3% |
| 3.5 – < 5.5 | 11 | 36.7% | 60.0% |
| 5.5 – < 7.5 | 7 | 23.3% | 83.3% |
| 7.5 – < 9.5 | 5 | 16.7% | 100.0% |
| **Total** | **30** | **100.0%** | |

The **cumulative relative frequency** column shows the percentage of observations up through (and including) that class. For example, 60% of calls were resolved in less than 5.5 minutes.
</div>

## Histograms

A **histogram** is a graphical representation of a frequency distribution for quantitative data. It uses adjacent vertical bars (rectangles) where:
- The **horizontal axis** shows the class intervals (bins)
- The **height of each bar** represents the frequency (or relative frequency) of observations in that class
- There are **no gaps** between bars (unlike bar charts)

The absence of gaps signals that the data is continuous — values flow from one class to the next without a break.

**Interpreting a histogram:** Look for:
- **Shape:** Is the distribution symmetric (bell-shaped), right-skewed (long tail to the right), or left-skewed?
- **Center:** Where is the bulk of the data?
- **Spread:** How wide is the distribution?
- **Outliers:** Are there isolated bars far from the main body of the data?

**Right-skewed** distributions (common with income, sales revenue, wait times) have a long tail extending to the right. The mean is pulled higher than the median. **Left-skewed** distributions have a long tail to the left. A **symmetric** distribution has tails of roughly equal length on both sides.

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Creating a Histogram Using the Data Analysis ToolPak:**

1. Enter your data in column A (e.g., A2:A31).
2. Create a "Bin" column in column B listing the upper boundary of each class: 3.5, 5.5, 7.5, 9.5.
3. Click **Data → Data Analysis → Histogram** → **OK**.
4. Set **Input Range** to your data (A2:A31), **Bin Range** to your bin column (B2:B5).
5. Check **Labels** if your range includes headers.
6. Under Output options, select **New Worksheet Ply** or choose an output range.
7. Check **Chart Output** to automatically generate a histogram chart.
8. Click **OK**.

**Formatting tip:** Right-click on one of the bars, select **Format Data Series**, and set the **Gap Width** to 0% to remove the gaps between bars (histograms should have no gaps).
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Histogram in Excel 2016+:** In Excel 2016 and later, you can insert a histogram directly: select your raw data, go to **Insert → Charts → Insert Statistic Chart → Histogram**. Excel automatically determines the bin widths. Right-click the horizontal axis and select **Format Axis** to customize the number of bins or set specific bin boundaries.
</div>

## Bar Charts

A **bar chart** (or bar graph) displays the frequency or relative frequency of **categorical** data. Each category has its own bar, and the **height** of the bar represents the category's count or percentage.

**Key differences between bar charts and histograms:**
- Bar charts: for **categorical** data; bars have **gaps** between them to emphasize that categories are distinct.
- Histograms: for **quantitative** continuous data; bars are **adjacent** to emphasize the continuous flow of values.

Bar charts can be displayed vertically (most common) or horizontally. Horizontal bar charts work well when category names are long.

**Best practices for bar charts:**
- Start the value axis at zero to avoid visually exaggerating differences.
- Sort bars by frequency (descending) if there is no natural ordering, to make the most common categories immediately visible.
- Label bars with values when the exact number matters.
- Use consistent colors; don't add colors just for decoration.

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Creating a Bar Chart in Excel:**

1. Select your frequency table (category labels and counts), for example A1:B5.
2. Go to **Insert → Charts** and select **Clustered Bar** (horizontal) or **Clustered Column** (vertical).
3. To sort bars by frequency: sort your frequency table in descending order before making the chart, or sort the table and the chart will update automatically.
4. Right-click the chart to access **Format Chart Area**, **Format Data Series**, and other customization options.
5. Add a chart title by clicking the chart, then **Chart Design → Add Chart Element → Chart Title**.
</div>

## Pie Charts

A **pie chart** displays parts of a whole as slices of a circle. Each slice's angle is proportional to its percentage of the total.

Pie charts are appropriate when:
- You have **categorical data**
- You want to show **parts of a whole** (proportions that sum to 100%)
- You have **few categories** (ideally 5 or fewer)
- The differences between categories are **substantial**

<div class="callout warning-box">
<span class="callout-title">Caution</span>
**When NOT to use pie charts:**

- When you have many categories (slices become too small to read)
- When differences between slices are small (humans are poor at comparing angles)
- When you want to compare multiple groups side-by-side
- When absolute values (not proportions) are what matters

Many data visualization experts recommend using a bar chart instead of a pie chart in most situations — bars are easier to read and compare accurately than slices. The pie chart is frequently misused. If you find yourself reaching for a pie chart, ask first: "Would a bar chart communicate this more clearly?"
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Creating a Pie Chart in Excel:**

1. Select your categories and their frequencies or percentages.
2. Go to **Insert → Charts → Pie** and choose **2-D Pie**.
3. Right-click on a slice and select **Add Data Labels**.
4. In **Format Data Labels**, check **Percentage** to show percentages instead of counts.
5. To explode a slice for emphasis, click a slice twice (slowly) to select just that slice, then drag it outward.
</div>

## Line Charts for Time Series

A **line chart** plots a variable over time, with time on the horizontal axis and the variable's value on the vertical axis. Points are connected by lines to emphasize the trend or pattern over time.

Line charts are ideal for:
- Showing trends (upward, downward, cyclical)
- Displaying seasonal patterns (retail sales spike in December)
- Comparing how two or more variables change over time

<div class="callout example-box">
<span class="callout-title">Example</span>
A coffee shop chain tracks average monthly sales revenue per location over 24 months. A line chart would immediately reveal whether revenue is trending upward, whether there are seasonal dips in summer, and whether revenue growth has been accelerating or flattening recently. These insights would be nearly impossible to extract from a table of 24 numbers.
</div>

**Best practices for line charts:**
- Always label the axes with the variable name and units.
- If showing multiple lines, use a legend and differentiate lines with color and/or line styles.
- Avoid using lines to connect categorical data (that creates a false impression of continuity).

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Creating a Line Chart in Excel:**

1. Enter your time labels (e.g., Jan, Feb, Mar…) in column A and your values in column B.
2. Select both columns and go to **Insert → Charts → Line → Line with Markers**.
3. Right-click the horizontal axis and select **Format Axis** if you need to adjust how dates or labels appear.
4. To add a trend line: right-click on the data series (the line itself), select **Add Trendline**, and choose from Linear, Exponential, Moving Average, etc. Check **Display R-squared value** to see how well the trend line fits.
</div>

## Scatter Plots

A **scatter plot** (or scatter diagram) displays the relationship between **two quantitative variables**. Each observation becomes a single point, with one variable on the horizontal axis ($x$) and the other on the vertical axis ($y$).

Scatter plots help answer questions like:
- Does advertising spending seem related to sales revenue?
- Do larger store locations generate more revenue?
- Is there a relationship between employee satisfaction and productivity?

When interpreting a scatter plot, note:
- **Direction:** Do the points trend upward (positive association) or downward (negative association), or is there no clear direction?
- **Strength:** Are the points clustered tightly along a line (strong relationship) or scattered loosely (weak relationship)?
- **Form:** Is the relationship roughly linear, or does it curve?
- **Outliers:** Are there any points far from the main cluster?

We study correlation and regression — the formal statistical follow-up to scatter plot analysis — in Chapter 12.

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Creating a Scatter Plot in Excel:**

1. Put your $x$-variable values in column A and your $y$-variable values in column B (same row for each observation).
2. Select both columns and go to **Insert → Charts → Scatter → Scatter (points only)**.
3. Label the axes: click the chart, then **Chart Design → Add Chart Element → Axis Titles**.
4. To add a regression line (trendline): right-click on any data point, select **Add Trendline → Linear**, and optionally check **Display Equation on chart** and **Display R-squared value on chart**.
</div>

## Principles of Good Data Visualization

A chart is a communication tool. Its purpose is to help the reader understand the data. Every design choice should serve that purpose. Here are the most important principles:

**1. Choose the right chart type.** Match the chart type to your data type and your question. Categorical data → bar or pie. Quantitative distribution → histogram. Time trend → line. Relationship between variables → scatter plot.

**2. Start the axis at zero (for bar charts).** When the vertical axis of a bar chart starts above zero, differences between bars are visually exaggerated. A bar that is twice as tall as another should represent twice as large a value — this only works if the axis starts at zero.

**3. Avoid chart junk.** "Chart junk" (a term coined by statistician Edward Tufte) refers to unnecessary visual elements that add clutter without adding information: excessive gridlines, decorative 3D effects, patterned fills, irrelevant background images. Simplicity serves clarity.

**4. Label everything.** Every chart needs: a title, labeled axes (with units), and a legend if there are multiple series. Never leave the reader guessing what a chart is about.

**5. Use color purposefully.** Color should encode information (e.g., different colors for different groups) or draw attention to something important. Do not add color just for decoration. Also, be aware that some readers may be color-blind; using both color and shape or pattern to differentiate series makes charts more accessible.

**6. Don't distort the data.** Using 3D effects, unusual axis scales, or truncated axes can make trends look steeper or differences look larger than they really are. Represent the data honestly.

<div class="callout warning-box">
<span class="callout-title">Caution</span>
**3D Charts:** Excel offers 3D versions of bar, pie, and other charts. Avoid them. 3D effects make it harder to accurately read values and compare categories. They add visual noise without adding information. Professional analysts and data visualization experts strongly recommend flat, clean, two-dimensional charts for accuracy and clarity.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Frequency Distribution</dt>
<dd>A table showing the number of observations falling into each category or class interval.</dd>

<dt>Relative Frequency</dt>
<dd>The proportion (or percentage) of observations in a given category or class; frequency divided by total observations.</dd>

<dt>Cumulative Frequency</dt>
<dd>The total frequency of all values up to and including a given class.</dd>

<dt>Class / Bin</dt>
<dd>An interval used to group quantitative data in a frequency distribution or histogram.</dd>

<dt>Histogram</dt>
<dd>A bar chart for quantitative data, where adjacent bars (no gaps) represent the frequency of values in each class interval.</dd>

<dt>Bar Chart</dt>
<dd>A chart for categorical data using separated bars to display the frequency or relative frequency of each category.</dd>

<dt>Pie Chart</dt>
<dd>A circular chart divided into slices representing each category's proportion of the total.</dd>

<dt>Line Chart</dt>
<dd>A chart connecting data points with lines, used to display trends or changes over time.</dd>

<dt>Scatter Plot</dt>
<dd>A chart plotting pairs of quantitative values as individual points, used to explore the relationship between two variables.</dd>

<dt>Skewness</dt>
<dd>A measure of asymmetry in a distribution. Right-skewed data has a long tail to the right; left-skewed data has a long tail to the left.</dd>

<dt>Chart Junk</dt>
<dd>Unnecessary visual elements in charts that add clutter without adding information, reducing clarity.</dd>
</dl>
</div>

---

## Exercises {-}

1. A convenience store tracks sales by product category during one week. The data (in dollars) are: Beverages \$1,240, Snacks \$890, Tobacco \$650, Lottery \$430, Other \$290.
   a. Create a **frequency distribution table** with relative frequencies.
   b. Construct a **bar chart** for this data in Excel (Insert → Column chart). Make sure to include a title and axis labels.
   c. Would a **pie chart** also be appropriate here? Create one in Excel and compare the two charts. Which communicates the information more effectively? Explain.

2. The following are purchase amounts (\$) for 25 online orders: 14, 47, 23, 88, 35, 62, 19, 74, 41, 56, 28, 93, 37, 65, 22, 51, 78, 33, 46, 17, 82, 59, 44, 71, 26.
   a. Construct a **frequency distribution** with 5 classes. Show the class boundaries, frequency, relative frequency, and cumulative relative frequency.
   b. Describe the **shape** of the distribution (symmetric, left-skewed, or right-skewed?).
   c. Use the **Data Analysis ToolPak** to create a histogram in Excel and compare it with your hand-constructed frequency distribution.

3. The quarterly revenues (in millions of dollars) for a regional retail chain over three years were:

   | Quarter | Year 1 | Year 2 | Year 3 |
   |---------|--------|--------|--------|
   | Q1 | 12.4 | 13.8 | 15.2 |
   | Q2 | 15.1 | 16.7 | 18.3 |
   | Q3 | 14.8 | 15.9 | 17.1 |
   | Q4 | 19.6 | 21.4 | 23.9 |

   a. Create a **line chart** in Excel showing revenue over all 12 quarters (label the horizontal axis Q1Y1 through Q4Y3).
   b. What **trend** is visible in the chart?
   c. What **seasonal pattern**, if any, is apparent?

4. A marketing analyst recorded monthly advertising spending and monthly sales revenue for 12 months:

   | Advertising (\$000) | 15 | 22 | 18 | 30 | 25 | 12 | 28 | 20 | 33 | 17 | 26 | 35 |
   |--------------------|----|----|----|----|----|----|----|----|----|----|----|-----|
   | Sales (\$000) | 142 | 198 | 171 | 253 | 221 | 118 | 238 | 187 | 274 | 155 | 215 | 298 |

   a. Create a **scatter plot** in Excel with advertising spending on the horizontal axis and sales revenue on the vertical axis.
   b. Describe the **direction** and approximate **strength** of the relationship between the two variables.
   c. Add a **linear trendline** to the scatter plot and display the equation and R² value. What does the R² value suggest?

5. Find a chart in a business news publication (such as the Wall Street Journal, Bloomberg, or a company's annual report). Print or save a copy.
   a. Identify the **chart type** and the **data type** being displayed.
   b. Evaluate the chart against at least **three principles of good visualization** discussed in this chapter. Does it follow them?
   c. Identify at least **one way** the chart could be improved. If possible, recreate an improved version in Excel.

6. *A company's annual report shows a bar chart of five-year revenue growth. The vertical axis starts at \$950 million and the highest bar reaches \$1,050 million. A graph of the same data with the axis starting at zero looks very different.*
   a. Calculate the percentage difference between the lowest bar (\$960M) and the highest bar (\$1,040M).
   b. With the axis starting at \$950M, approximately how many times taller does the highest bar appear compared to the lowest bar in that chart?
   c. What is the ethical concern with truncating the axis in this way? In what context might it be acceptable?
