# Data Types and Collection {#data}

## Data Is the Raw Material of Statistics

Before you can calculate a single statistic, you need data. But not all data is the same. The type of data you have determines which statistical methods are appropriate, which Excel functions to use, and even which graphs make sense. A manager who tries to compute the average of a list of customer favorite colors is making a fundamental error. Understanding data types is the foundation upon which everything else in statistics rests.

In this chapter, we examine the major types of data, how to collect data properly, and the common sources of error that can ruin even a beautifully designed analysis.

## Qualitative vs. Quantitative Data

The most fundamental distinction in data is between data that consists of **categories** and data that consists of **numbers**.

**Qualitative data** (also called **categorical data**) describes characteristics or attributes. The values are labels or names — they fall into categories rather than on a numeric scale.

Examples of qualitative data in business:
- A customer's payment method (cash, credit card, debit card, mobile payment)
- An employee's department (Marketing, Finance, Operations, HR)
- A product's color or size category (Small, Medium, Large)
- A customer's satisfaction rating expressed as a word (Excellent, Good, Fair, Poor)
- Industry classification of a company (Retail, Manufacturing, Technology, Healthcare)

**Quantitative data** consists of numerical measurements or counts on which arithmetic operations make sense.

Examples of quantitative data in business:
- Annual salary of an employee (\$58,400)
- Number of units sold in a week (342 units)
- Time to fulfill a customer order (4.7 hours)
- Customer age (27 years)
- Return on investment (12.3%)

The key test for quantitative data: does it make sense to add, subtract, multiply, or average the values? It makes sense to compute the average salary but not the "average department."

## Levels of Measurement

Within these two broad categories, data can be further classified into four **levels of measurement**, each offering more information than the previous. Understanding the level of measurement tells you exactly which statistical operations are valid.

### Nominal Scale

The **nominal** level is the simplest. Data at this level are categories with no inherent order or ranking. The only thing you can say about two nominal values is whether they are the same or different.

Business examples:
- Store location codes: Store A, Store B, Store C (no store is inherently "higher" than another)
- Product category: Apparel, Electronics, Home Goods
- Customer gender identity
- Brand preference: Brand X, Brand Y, Brand Z

What you can do with nominal data: count frequencies, compute percentages, find the mode (most common category).

What you cannot do: rank the categories, compute an average, or say one category is "more" than another.

### Ordinal Scale

The **ordinal** level adds the ability to rank or order categories. The categories have a meaningful sequence, but the **distances between categories are not necessarily equal**.

Business examples:
- Customer satisfaction: Very Dissatisfied, Dissatisfied, Neutral, Satisfied, Very Satisfied
- Employee performance rating: Below Expectations, Meets Expectations, Exceeds Expectations
- Credit risk rating: AAA, AA, A, BBB, BB, B (bond ratings)
- Education level: High School, Some College, Bachelor's Degree, Graduate Degree

What you can do: rank observations, find the median, compare whether one value is higher or lower than another.

What you cannot do: say the gap between "Neutral" and "Satisfied" is the same as the gap between "Satisfied" and "Very Satisfied" — those gaps are undefined.

<div class="callout note-box">
<span class="callout-title">Note</span>
Likert-scale survey responses (such as 1 = Strongly Disagree through 5 = Strongly Agree) are technically ordinal data. In practice, business researchers often treat them as interval data and compute averages for the sake of convenience. This is a common compromise, but you should be aware that it involves an assumption that the scale intervals are equal — an assumption that may not be perfectly justified.
</div>

### Interval Scale

The **interval** level has all the properties of ordinal data, plus the distances between values are **equal and meaningful**. You can meaningfully say that the gap between 70°F and 80°F is the same as the gap between 80°F and 90°F.

However, interval scales lack a **true zero point**. A value of zero does not mean "none" of the quantity — it is just another point on the scale.

Business examples:
- Year (the year 2000 is not "twice" the year 1000 in any meaningful sense)
- Temperature in Fahrenheit or Celsius (0°F does not mean "no heat")
- IQ scores
- Index values (a stock market index of 0 would not mean "no stock value")

What you can do: compute means, standard deviations, and most arithmetic operations. The differences between values are meaningful.

What you cannot do: form ratios. A temperature of 80°F is not "twice as hot" as 40°F in any physical sense.

### Ratio Scale

The **ratio** level is the richest level of measurement. It has all the properties of interval data, plus a **true zero point**, which means zero really does mean "none" of the quantity. This allows meaningful ratio comparisons.

Business examples:
- Revenue (\$0 revenue means no revenue at all; \$200,000 is twice \$100,000)
- Number of employees (0 employees means no employees)
- Weight of shipment
- Time to complete a task (0 minutes means it took no time)
- Age

What you can do: all arithmetic operations, including ratios. "This product line generates three times the revenue of that one" is a meaningful statement.

The table below summarizes the four levels:

| Level | Order? | Equal Intervals? | True Zero? | Example |
|-------|--------|-----------------|-----------|---------|
| Nominal | No | No | No | Payment method |
| Ordinal | Yes | No | No | Satisfaction rating |
| Interval | Yes | Yes | No | Calendar year |
| Ratio | Yes | Yes | Yes | Sales revenue |

## Cross-Sectional vs. Time-Series Data

Data can also be classified by how it is collected over time.

**Cross-sectional data** is collected from multiple subjects **at a single point in time** (or a single time period treated as a snapshot). It provides a picture of how things differ across subjects at one moment.

Example: Recording the Q3 sales revenue for each of 50 retail stores. Each store is observed once; we are comparing stores at the same point in time.

**Time-series data** is collected from **one or more subjects at multiple points in time**. It tracks how something changes over time.

Example: Recording monthly revenue for a single retail store over 36 consecutive months. We are watching how that store's revenue evolves over time.

Many business data sets are actually both: recording multiple variables for multiple subjects over multiple time periods (called **panel data** or **longitudinal data**). For this course, we focus primarily on cross-sectional data, with time-series data appearing mainly in data visualization (line charts, Chapter 4).

## Primary vs. Secondary Data

Data can also be classified by its origin.

**Primary data** is data collected directly by the researcher for the specific purpose of a study. It is fresh, tailored to your question, and you control how it is collected. The downside: it takes time and money.

Examples:
- A company conducts a customer satisfaction survey
- A researcher observes how long customers spend in different store departments
- A firm runs a controlled experiment with two versions of a product

**Secondary data** is data that already exists, collected by someone else for some other purpose. It is faster and cheaper to obtain, but may not fit your question perfectly.

Examples:
- U.S. Census Bureau economic data
- Industry trade association reports
- A company's own internal sales records from prior years
- Nielsen market research reports
- Data purchased from a data broker

<div class="callout note-box">
<span class="callout-title">Note</span>
Secondary data sources can be tremendously valuable — government statistical agencies produce enormous quantities of free, reliable business data. However, always evaluate secondary data carefully: When was it collected? By whom? For what purpose? How was it measured? Data collected for one purpose may have definitions or categories that do not match your needs.
</div>

## Sampling Methods

When we collect primary data from a sample rather than a census (complete enumeration of the population), the method we use to select the sample matters enormously. A **probability sample** gives every member of the population a known, nonzero chance of being selected. This is what allows us to make valid statistical inferences. A **non-probability sample** does not provide this guarantee.

### Simple Random Sampling

In **simple random sampling**, every member of the population has an **equal probability** of being selected, and every possible sample of size $n$ has an equal probability of being the one chosen.

How to do it: Assign a number to every member of the population, then use a random number generator to select $n$ numbers. Excel can generate random numbers with the `=RAND()` function or the **Data Analysis ToolPak's** Random Number Generation tool.

Example: A company has 2,000 customers. To survey 100, they number the customers 1 to 2,000 and use Excel to randomly select 100 numbers.

Advantage: No bias in selection; results are generalizable to the population.
Disadvantage: Requires a complete list (sampling frame) of the population, which is not always available.

### Systematic Sampling

In **systematic sampling**, you select every $k$th member of a list after a random starting point. Here, $k = N/n$ (population size divided by desired sample size).

Example: A supermarket receives a shipment of 1,000 boxes of cereal and wants to inspect 50. $k = 1000/50 = 20$. They randomly choose a starting point (say, box number 7) and then select every 20th box: 7, 27, 47, 67, …

Advantage: Easy to implement; no complete list required ahead of time.
Disadvantage: If the population has a periodic pattern aligned with $k$, results can be biased (rare in business settings, but worth knowing).

### Stratified Sampling

In **stratified sampling**, the population is divided into subgroups called **strata** (based on some characteristic), and a random sample is drawn from each stratum.

Example: A company wants to survey employee satisfaction. They know that job satisfaction may differ between full-time and part-time employees. They divide (stratify) their 1,000 employees into 700 full-time and 300 part-time, then randomly sample 70 from full-time and 30 from part-time — maintaining the 70/30 proportional split.

Advantage: Ensures representation from all key subgroups; often produces more precise estimates than simple random sampling for the same sample size.
Disadvantage: Requires knowing the strata in advance; more complex to administer.

### Cluster Sampling

In **cluster sampling**, the population is divided into clusters (often based on natural groupings like geographic areas), a random sample of clusters is selected, and then **all** members of the chosen clusters are studied.

Example: A retailer with 200 store locations wants to survey customers. Rather than sampling customers across all stores, they randomly select 20 stores (clusters) and survey all customers at those 20 stores on a given day.

Advantage: Convenient and cost-effective when the population is spread over a large geographic area.
Disadvantage: Members within a cluster tend to be similar to each other, which can reduce the efficiency of the sample relative to simple random sampling.

### Convenience Sampling

**Convenience sampling** (a non-probability method) involves selecting whoever is most easily available or accessible.

Example: A professor surveys her three statistics classes to study student study habits. An online retailer surveys only customers who click on a post-purchase pop-up. A market researcher asks shoppers at one mall location.

Advantage: Fast and cheap.
Disadvantage: **High risk of bias.** The people most conveniently available may differ systematically from the broader population. Results cannot be reliably generalized. Convenience samples are fine for exploratory work but should not be used for formal statistical inference.

<div class="callout warning-box">
<span class="callout-title">Caution</span>
Most online surveys, social media polls, and "call-in" surveys are convenience samples. The people who respond are self-selected — they differ from non-respondents in ways that may be directly related to the question being asked. Be very skeptical of statistics based on convenience samples, especially when they appear in news stories and marketing claims.
</div>

## Surveys and Questionnaire Design

Many business data-collection efforts involve surveys. Writing good survey questions is harder than it looks. Here are key principles:

**1. Ask one thing at a time.** Avoid double-barreled questions: "Do you find our product affordable and easy to use?" (What if it's affordable but difficult?) Ask two separate questions.

**2. Use neutral language.** Avoid leading questions: "Don't you agree that our customer service is excellent?" The phrasing pushes respondents toward a positive answer. Better: "How would you rate our customer service? (Excellent / Good / Fair / Poor)"

**3. Keep it simple.** Use plain, common language. Avoid jargon or technical terms that respondents may not understand.

**4. Provide exhaustive and mutually exclusive response options.** For a multiple-choice question about customer age, the categories should cover all possible ages and should not overlap: "Under 18 / 18–34 / 35–54 / 55 or older" works. "18–35 / 35–50 / 50+" does not work because age 35 and 50 fall in two categories.

**5. Consider response order effects.** The order in which options are presented can influence responses. When possible, randomize the order of response options across respondents.

**6. Keep the survey short.** Response rates and data quality drop sharply as surveys get longer. Focus on only the questions you truly need.

## Sources of Bias

**Bias** is a systematic error that causes results to consistently differ from the truth. Unlike random error (which averages out over large samples), bias does not disappear with a larger sample — it persists and corrupts your conclusions.

Common sources of bias in business data collection:

**Selection bias:** The sample is not representative because of how subjects were selected. Example: Surveying only customers who call to complain will overstate dissatisfaction.

**Non-response bias:** People who don't respond to a survey differ systematically from those who do. Example: Happier employees may be less likely to respond to an engagement survey, skewing results toward dissatisfaction.

**Response bias (or social desirability bias):** Respondents give answers they think are expected or socially acceptable rather than their true opinions or behaviors. Example: Employees may underreport time spent on non-work activities when surveyed by HR.

**Measurement bias:** The measurement instrument itself introduces systematic error. Example: A scale that consistently reads 0.5 kg too high will bias weight measurements upward.

**Interviewer bias:** The characteristics or behavior of the interviewer influence responses. Example: Respondents may answer differently when surveyed in person versus anonymously online.

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Importing Data:** To import a CSV (comma-separated values) file into Excel: go to **Data → Get Data → From Text/CSV**, navigate to your file, and follow the import wizard. Excel will preview how the data will be parsed. For data already in Excel format (.xlsx), simply open the file normally.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Sorting Data:** To sort a column, select any cell in the column, then click **Data → Sort A to Z** (ascending) or **Sort Z to A** (descending). To sort by multiple columns simultaneously (e.g., first by department, then by last name within department), use **Data → Sort** to open the multi-level sort dialog.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Filtering Data:** To filter rows based on criteria, select any cell in your data and click **Data → Filter**. Drop-down arrows appear in each column header. Click a drop-down to filter by specific values, or use **Number Filters** / **Text Filters** for more complex conditions like "greater than 100" or "contains 'East'." Click **Clear** to remove filters and show all rows.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Generating Random Numbers for Simple Random Sampling:** In an empty column next to your list, type `=RAND()` in the first cell and copy it down for all rows. This generates a random number between 0 and 1 for each row. Then sort the entire data set by this random-number column. The top $n$ rows after sorting are your simple random sample. Note: `=RAND()` recalculates every time Excel recalculates, so **paste as values** (Paste Special → Values) to freeze the random numbers once you've made your selection.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Qualitative (Categorical) Data</dt>
<dd>Data whose values are labels or category names rather than numbers; describes attributes or characteristics.</dd>

<dt>Quantitative Data</dt>
<dd>Data consisting of numerical measurements or counts on which arithmetic operations make sense.</dd>

<dt>Nominal Scale</dt>
<dd>The simplest level of measurement; data are categories with no inherent order.</dd>

<dt>Ordinal Scale</dt>
<dd>A level of measurement where categories have a meaningful order but the intervals between categories are not necessarily equal.</dd>

<dt>Interval Scale</dt>
<dd>A level of measurement with equal, meaningful intervals between values, but no true zero point.</dd>

<dt>Ratio Scale</dt>
<dd>The highest level of measurement; has equal intervals AND a true zero point, allowing meaningful ratio comparisons.</dd>

<dt>Cross-Sectional Data</dt>
<dd>Data collected from multiple subjects at a single point in time.</dd>

<dt>Time-Series Data</dt>
<dd>Data collected from one or more subjects at multiple points in time, tracking change over time.</dd>

<dt>Primary Data</dt>
<dd>Data collected directly by the researcher for the specific purpose of the current study.</dd>

<dt>Secondary Data</dt>
<dd>Data already collected by others for some other purpose, repurposed for the current study.</dd>

<dt>Simple Random Sample</dt>
<dd>A sample in which every member of the population has an equal chance of being selected.</dd>

<dt>Stratified Sample</dt>
<dd>A sample obtained by dividing the population into subgroups (strata) and randomly sampling from each.</dd>

<dt>Cluster Sample</dt>
<dd>A sample obtained by dividing the population into clusters, randomly selecting clusters, and studying all members of those clusters.</dd>

<dt>Bias</dt>
<dd>A systematic error in data collection or analysis that causes results to consistently deviate from the truth in one direction.</dd>
</dl>
</div>

---

## Exercises {-}

1. Classify each of the following variables as **qualitative** or **quantitative**. For quantitative variables, also state whether they are **discrete** or **continuous**. For qualitative variables, state whether they are **nominal** or **ordinal**.
   a. Number of customer complaints received per day
   b. A restaurant's cleanliness rating: Excellent, Good, Needs Improvement
   c. The zip code of a customer's billing address
   d. The time (in minutes) a customer waits on hold before reaching a service representative
   e. An employee's annual performance bonus (\$)
   f. The type of industry a company operates in

2. For each variable below, identify the **level of measurement** (nominal, ordinal, interval, ratio) and justify your answer:
   a. A product's star rating on an e-commerce site (1–5 stars)
   b. Temperature in a warehouse measured in degrees Fahrenheit
   c. The year a business was founded
   d. Total revenue generated by a sales representative (\$)
   e. A customer's membership tier: Bronze, Silver, Gold, Platinum

3. A regional grocery chain wants to estimate the average weekly spending per household in its loyalty card program. The company has records for 180,000 cardholders.
   a. What is the population of interest?
   b. Describe how you would obtain a **simple random sample** of 500 cardholders using Excel.
   c. Could a **stratified sample** improve this study? If so, what variable would you use to form strata? Explain why.

4. A market research firm wants to survey shoppers about a new product concept. They set up a table at a suburban shopping mall on a Tuesday afternoon and invite passing shoppers to participate.
   a. What type of sampling method is this?
   b. Identify at least **three specific ways** this approach could produce a biased sample.
   c. Suggest a better sampling method for this study and explain why it would be an improvement.

5. Evaluate the following survey questions. For each one, identify the problem and rewrite the question to correct it:
   a. "Do you agree that our return policy is fair and easy to understand?"
   b. "How many times have you visited our website in the past 30 days?" (Response options: 0–5 / 5–10 / 10–20 / 20+)
   c. "Our employees work very hard to serve you. How satisfied were you with our service today?"

6. *A national bank wants to study the financial behaviors of small business owners. They plan to mail a survey to 2,000 randomly selected small business owners from their commercial customer database. Only 320 respond.*
   a. What is the **response rate**?
   b. What type of bias is most likely present in the 320 responses? Explain your reasoning.
   c. How might this bias affect the bank's conclusions about small business financial behavior?
