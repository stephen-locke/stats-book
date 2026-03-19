# Introduction to Probability {#probability}

## Uncertainty Is the Business Condition

Every business decision involves uncertainty. Will this product sell? Will a loan be repaid? Will a shipment arrive on time? Will a new hire succeed? The tools of probability give us a principled, mathematical way to reason about uncertainty — to move from "I have no idea" to "based on evidence, there is a 73% chance of this outcome."

Probability is the mathematical foundation of statistics. The concepts in this chapter underlie every inferential procedure in the rest of the book: confidence intervals, hypothesis tests, and regression inference all depend on probability reasoning. More immediately, probability appears directly in business decisions: insurance pricing, quality control, supply chain management, and financial risk analysis all rely on probability calculations.

## Basic Probability Concepts

### Experiments, Outcomes, and Sample Spaces

A **probability experiment** (or random experiment) is any process that produces an outcome that cannot be predicted with certainty in advance.

Examples:
- Rolling a die
- Randomly selecting a customer from a database
- Testing a manufactured item to see if it is defective
- Recording whether the next customer pays with cash or card

An **outcome** is a single possible result of an experiment.

The **sample space** ($S$) is the set of all possible outcomes of an experiment.

| Experiment | Possible Outcomes | Sample Space |
|------------|-------------------|-------------|
| Flip a coin | Heads, Tails | $S = \{H, T\}$ |
| Roll a six-sided die | 1, 2, 3, 4, 5, 6 | $S = \{1, 2, 3, 4, 5, 6\}$ |
| Classify a customer complaint | Billing, Shipping, Quality, Other | $S = \{B, S, Q, O\}$ |
| Record whether item is defective | Defective, Not defective | $S = \{D, ND\}$ |

An **event** is any subset of the sample space — one or more outcomes grouped together because they satisfy some condition of interest.

Example: Rolling a die and defining event $A$ = "roll an even number." Then $A = \{2, 4, 6\}$, which is a subset of $S = \{1, 2, 3, 4, 5, 6\}$.

### The Probability of an Event

The **probability** of an event $A$, written $P(A)$, is a number between 0 and 1 that represents the likelihood of that event occurring.

- $P(A) = 0$ means the event is impossible.
- $P(A) = 1$ means the event is certain.
- $P(A) = 0.5$ means the event is equally likely to occur or not occur.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Basic Probability Properties:**
1. $0 \leq P(A) \leq 1$ for any event $A$
2. $P(S) = 1$ (the probability of some outcome in the sample space is 1)
3. $\sum_{\text{all outcomes}} P(\text{outcome}) = 1$
</div>

## Classical, Empirical, and Subjective Probability

There are three ways to assign a probability to an event.

### Classical Probability

**Classical probability** applies when all outcomes in the sample space are **equally likely**. The probability of an event is the number of favorable outcomes divided by the total number of outcomes.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$P(A) = \frac{\text{Number of outcomes in event } A}{\text{Total number of outcomes in the sample space}} = \frac{n(A)}{n(S)}$$
</div>

**Example:** A raffle has 500 tickets, and you bought 20. What is the probability you win?
$$P(\text{win}) = \frac{20}{500} = 0.04 = 4\%$$

### Empirical Probability

**Empirical probability** (also called relative frequency probability) is based on observed data from past experiments or historical records. You run the experiment many times and use the proportion of times the event occurred as the probability.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$P(A) = \frac{\text{Number of times event } A \text{ occurred}}{\text{Total number of trials}}$$
</div>

**Example:** A manufacturer's quality records show that 37 out of 2,000 items produced last week were defective. Based on this history:
$$P(\text{defective}) = \frac{37}{2000} = 0.0185 = 1.85\%$$

This empirical probability can now be used for planning: in a production run of 10,000 units, we'd expect approximately $10,000 \times 0.0185 = 185$ defective items.

### Subjective Probability

**Subjective probability** is a personal assessment of the likelihood of an event, based on expert judgment, experience, or incomplete information. It does not require historical data or equally likely outcomes.

Examples:
- A venture capitalist estimates a 30% chance that a startup will achieve profitability within two years.
- A project manager believes there is a 70% probability that the project will be completed on time.
- An analyst forecasts a 40% chance of a recession in the next 12 months.

Subjective probabilities are common in business because many decisions involve novel situations where historical data is limited. They are legitimate as long as they are consistent with probability rules.

## The Complement Rule

The **complement** of event $A$ (written $A^c$ or $\bar{A}$) is the set of all outcomes in the sample space that are NOT in $A$. Since every outcome either is or is not in $A$:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$P(A^c) = 1 - P(A)$$
</div>

**Example:** If there is a 15% chance that a customer will request a refund, then there is a $(1 - 0.15) = 85\%$ chance they will not request a refund.

The complement rule is surprisingly useful — sometimes it is much easier to compute the probability of "not A" and subtract from 1.

## The Addition Rule

The **addition rule** finds the probability that event $A$ **OR** event $B$ occurs (or both).

### Mutually Exclusive Events

Events $A$ and $B$ are **mutually exclusive** (also called disjoint) if they cannot both occur at the same time. If $A$ happens, $B$ cannot happen, and vice versa.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Addition Rule for Mutually Exclusive Events:**
$$P(A \text{ or } B) = P(A) + P(B)$$
</div>

**Example:** A customer calls customer service. Based on past data, the probability the issue is a billing problem is 0.35, and the probability it is a shipping problem is 0.28. (A call cannot be classified as both.) What is the probability of either a billing or shipping issue?
$$P(\text{billing or shipping}) = 0.35 + 0.28 = 0.63$$

### General Addition Rule (Non-Mutually Exclusive Events)

When events $A$ and $B$ **can both occur at the same time**, simply adding $P(A) + P(B)$ double-counts the outcomes where both occur. We subtract the overlap:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**General Addition Rule:**
$$P(A \text{ or } B) = P(A) + P(B) - P(A \text{ and } B)$$
</div>

**Example:** At a company, 60% of employees have a college degree, 40% have more than 5 years of experience, and 25% have both. What is the probability that a randomly selected employee has a degree OR more than 5 years of experience?
$$P(\text{degree or experience}) = 0.60 + 0.40 - 0.25 = 0.75$$

## The Multiplication Rule

The **multiplication rule** finds the probability that event $A$ **AND** event $B$ both occur.

### Independent Events

Events $A$ and $B$ are **independent** if the occurrence of one does not affect the probability of the other.

<div class="callout formula-box">
<span class="callout-title">Formula</span>
**Multiplication Rule for Independent Events:**
$$P(A \text{ and } B) = P(A) \times P(B)$$
</div>

**Example:** A supplier has a 5% defect rate. You receive two separate shipments from this supplier. What is the probability that both shipments contain at least one defective item? (Assuming shipments are independent.)
$$P(\text{both defective}) = 0.05 \times 0.05 = 0.0025 = 0.25\%$$

### Dependent Events and Conditional Probability

Events $A$ and $B$ are **dependent** if the occurrence of one affects the probability of the other. In this case, we need **conditional probability**.

The **conditional probability** of event $B$ given that event $A$ has already occurred is:

<div class="callout formula-box">
<span class="callout-title">Formula</span>
$$P(B \mid A) = \frac{P(A \text{ and } B)}{P(A)}$$

Read "$P(B \mid A)$" as "the probability of $B$ given $A$."

**General Multiplication Rule (for dependent events):**
$$P(A \text{ and } B) = P(A) \times P(B \mid A)$$
</div>

**Example:** A shipment contains 20 items, of which 3 are defective. Two items are drawn **without replacement** (dependent events, because removing the first item changes the composition of the remaining items).

$P(\text{1st is defective}) = 3/20 = 0.15$

$P(\text{2nd is defective} \mid \text{1st was defective}) = 2/19$ (only 2 defective remain out of 19 items)

$P(\text{both defective}) = \frac{3}{20} \times \frac{2}{19} = \frac{6}{380} \approx 0.0158$

## Contingency Tables

A **contingency table** (also called a cross-tabulation or two-way table) displays joint frequencies for two categorical variables simultaneously. It is one of the most useful tools for computing probabilities from observed data.

<div class="callout example-box">
<span class="callout-title">Example</span>
A retail company surveys 400 customers about their preferred shopping channel and their age group.

| | Under 35 | 35 or Older | **Total** |
|-|---------|------------|---------|
| **Online** | 140 | 80 | **220** |
| **In-Store** | 60 | 120 | **180** |
| **Total** | **200** | **200** | **400** |

The **joint probability** of two events is the probability they both occur. Here, the probability that a randomly selected customer is under 35 AND prefers online shopping:
$$P(\text{Under 35 and Online}) = \frac{140}{400} = 0.35$$

A **marginal probability** is the probability of a single event, obtained from the row or column totals:
$$P(\text{Online}) = \frac{220}{400} = 0.55 \qquad P(\text{Under 35}) = \frac{200}{400} = 0.50$$

A **conditional probability** asks: given that the customer is under 35, what is the probability they prefer online shopping?
$$P(\text{Online} \mid \text{Under 35}) = \frac{140}{200} = 0.70$$

Compare to: $P(\text{Online} \mid \text{35 or older}) = 80/200 = 0.40$.

The fact that these conditional probabilities differ (0.70 vs. 0.40) tells us that shopping channel preference is **not independent** of age — younger customers are much more likely to prefer online shopping.
</div>

**Testing for independence using a contingency table:**
Events $A$ and $B$ are independent if and only if:
$$P(A \mid B) = P(A) \qquad \text{equivalently, } P(A \text{ and } B) = P(A) \times P(B)$$

If $P(\text{Online} \mid \text{Under 35}) = 0.70 \neq P(\text{Online}) = 0.55$, the events are dependent.

## Tree Diagrams

A **tree diagram** is a visual tool for computing probabilities of sequences of events, especially when events are dependent or when there are multiple stages.

Each **branch** of the tree represents one possible outcome at a stage. The probability of any path through the tree is the product of the probabilities along that path.

<div class="callout example-box">
<span class="callout-title">Example</span>
A software company finds that 70% of sales calls result in a scheduled demo, and 40% of demos result in a sale. For a randomly selected initial sales call:

**Stage 1:** Call leads to a demo (probability 0.70) or no demo (probability 0.30).

**Stage 2 (given demo):** Demo leads to a sale (probability 0.40) or no sale (probability 0.60).

| Path | Probability |
|------|-------------|
| Demo AND Sale | $0.70 \times 0.40 = 0.28$ |
| Demo AND No Sale | $0.70 \times 0.60 = 0.42$ |
| No Demo | $0.30 \times 1.00 = 0.30$ |
| **Total** | **1.00** |

The probability that a random sales call ultimately results in a sale is **0.28 or 28%**.
</div>

## Excel for Probability Calculations

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Basic Probability Calculations in Excel:**

Excel does not have a dedicated "probability" function for the basic rules, but you can use cell arithmetic. For example:

- Complement rule: If P(A) is in cell B2, then `=1-B2` gives $P(A^c)$.
- Addition rule: If P(A) is in B2, P(B) is in B3, and P(A and B) is in B4, then `=B2+B3-B4` gives $P(A \text{ or } B)$.
- Multiplication rule (independent): `=B2*B3` gives $P(A \text{ and } B)$.

For contingency tables: enter the joint frequency table into a spreadsheet. Use `=B2/SUM(B$2:B$5)` style formulas (with mixed references) to convert counts to probabilities. This makes it easy to compute all joint, marginal, and conditional probabilities from one table.
</div>

<div class="callout excel-tip">
<span class="callout-title">Excel Tip</span>
**Using COUNTIF for Empirical Probability:** If your data is in column A (a list of outcomes), use `=COUNTIF(A:A, "outcome")` to count how many times a specific outcome occurred, then divide by `=COUNT(A:A)` to get the empirical probability.

Example: If column A contains 1,000 rows of "Pass" or "Fail" quality test results:
`=COUNTIF(A2:A1001,"Fail")/COUNT(A2:A1001)` gives the empirical probability of a failure.

For numeric data, use `=COUNTIF(A2:A1001,">100")/COUNT(A2:A1001)` to find the proportion of values greater than 100.
</div>

---

<div class="callout key-terms">
<span class="callout-title">Key Terms</span>
<dl>
<dt>Probability Experiment</dt>
<dd>A process that produces an outcome that cannot be predicted with certainty in advance.</dd>

<dt>Sample Space ($S$)</dt>
<dd>The set of all possible outcomes of a probability experiment.</dd>

<dt>Event</dt>
<dd>A subset of the sample space; one or more outcomes that share a condition of interest.</dd>

<dt>Classical Probability</dt>
<dd>Probability computed by dividing the number of favorable outcomes by the total number of equally likely outcomes.</dd>

<dt>Empirical Probability</dt>
<dd>Probability estimated from observed frequencies in historical data.</dd>

<dt>Subjective Probability</dt>
<dd>A personal estimate of the probability of an event, based on judgment rather than equal outcomes or historical data.</dd>

<dt>Complement ($A^c$)</dt>
<dd>The event that $A$ does NOT occur; $P(A^c) = 1 - P(A)$.</dd>

<dt>Mutually Exclusive Events</dt>
<dd>Events that cannot both occur at the same time; $P(A \text{ and } B) = 0$.</dd>

<dt>Independent Events</dt>
<dd>Events where the occurrence of one has no effect on the probability of the other; $P(B \mid A) = P(B)$.</dd>

<dt>Conditional Probability</dt>
<dd>The probability of an event given that another event has already occurred: $P(B \mid A) = P(A \text{ and } B)/P(A)$.</dd>

<dt>Joint Probability</dt>
<dd>The probability that two events both occur: $P(A \text{ and } B)$.</dd>

<dt>Marginal Probability</dt>
<dd>The overall probability of a single event, obtained from the totals in a contingency table.</dd>

<dt>Contingency Table</dt>
<dd>A table showing the joint frequency distribution of two categorical variables.</dd>

<dt>Tree Diagram</dt>
<dd>A visual tool for computing probabilities of multi-stage processes by tracing paths through branches.</dd>
</dl>
</div>

---

## Exercises {-}

1. A retail store records the number of customers who make a purchase versus those who browse without buying over 500 visits: 320 make a purchase, 180 do not.
   a. What is the empirical probability that a random customer makes a purchase?
   b. What is the probability that a random customer does NOT make a purchase?
   c. If a second customer walks in independently, what is the probability that both customers make a purchase?

2. At a manufacturing plant, the probability that a machine needs maintenance on any given day is 0.12. On any given day, there are three machines operating independently.
   a. What is the probability that none of the three machines need maintenance?
   b. What is the probability that at least one machine needs maintenance? (Use the complement rule.)
   c. What is the probability that all three machines need maintenance?

3. A survey of 300 small business owners asked about their primary concern. Results: Cash flow (105), Competition (75), Finding talent (60), Regulation (45), Other (15).
   a. Construct a probability distribution table (list each concern with its empirical probability).
   b. Verify that the probabilities sum to 1.
   c. What is the probability that a randomly selected owner's primary concern is either cash flow or competition?

4. Use the following contingency table, which shows customer satisfaction ratings by purchase channel for 500 customers:

   | | Online | In-Store | **Total** |
   |-|--------|----------|---------|
   | **Satisfied** | 165 | 180 | **345** |
   | **Unsatisfied** | 85 | 70 | **155** |
   | **Total** | **250** | **250** | **500** |

   a. Find: $P(\text{Satisfied})$, $P(\text{Online})$, $P(\text{Satisfied and Online})$.
   b. Find: $P(\text{Satisfied} \mid \text{Online})$ and $P(\text{Satisfied} \mid \text{In-Store})$.
   c. Are channel (Online vs. In-Store) and satisfaction independent? Justify using the independence test.

5. A consulting firm is bidding on two contracts simultaneously. They estimate a 55% chance of winning Contract A and a 40% chance of winning Contract B. They believe the two outcomes are independent.
   a. What is the probability of winning both contracts?
   b. What is the probability of winning at least one contract? (Use the general addition rule, or use the complement rule.)
   c. What is the probability of winning neither contract?

6. A credit card company uses a fraud detection model. It flags 8% of transactions as potentially fraudulent. Of transactions that are truly fraudulent, the model flags 90% of them. Of transactions that are not fraudulent, the model flags 5% of them. Suppose 2% of all transactions are truly fraudulent.
   a. Draw a **tree diagram** with two stages: (1) Is the transaction truly fraudulent? (2) Does the model flag it?
   b. Find the probability that a randomly selected transaction is: fraudulent AND flagged, not fraudulent AND flagged, not fraudulent AND not flagged, fraudulent AND not flagged.
   c. Verify that your four probabilities sum to 1.
   d. If a transaction is flagged by the model, what is the probability it is truly fraudulent? (This is the key business question! Show your work carefully.)

7. *An e-commerce company runs an A/B test on its checkout page. Version A (current) has a 4.2% conversion rate. Version B (new design) has a 5.8% conversion rate (based on a sample test). In a given hour, 300 visitors see Version A and 300 see Version B. What is the probability that at least one conversion occurs from the Version A visitors? What about Version B? (Assume each visitor converts independently, and use the complement rule.)*

8. *A project manager must complete three sequential phases of a project. The probability of completing Phase 1 on time is 0.90. Given Phase 1 is completed on time, the probability of completing Phase 2 on time is 0.80. Given both Phase 1 and Phase 2 are on time, the probability of completing Phase 3 on time is 0.75. What is the probability the entire project is completed on time? Draw a tree diagram and label all branches.*
