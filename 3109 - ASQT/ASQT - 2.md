---
course: "CSE 3109: Applied Statistics and Queuing Theory (ASQT)"
class: "ASQT - 2"
duration: "1:09:14"
---
# ASQT - 2: Sampling Methods, Data & Variable Classification, Measurement Scales, and Frequency Distributions

## Overview
This lecture bridges the foundational concepts from Class 1 (population vs. sample, parameters vs. statistics, and sampling/non-sampling errors) into practical statistical data handling. The teacher first covered four sampling methods, then introduced variables, constants, data types, and the four levels of measurement (nominal, ordinal, interval, and ratio). In the second half, the class covered data sets, tabular structure, data quality issues, data collection sources, and organizing raw data into arrays and ungrouped or grouped frequency distributions (including class boundaries, the left-end convention, and rules for choosing the number of classes).

## Topic Map
- Recap of Class 1
  - Population vs. sample and practical limitations
  - Parameters vs. statistics and error accounting
  - References to Class 1 symbols and error concepts
- Sampling Approaches
  - Random sampling (sampling frame, pros/cons)
  - Systematic sampling ($k$-th element selection)
  - Stratified sampling (strata and random sampling within groups)
  - Cluster sampling (whole cluster as a sample)
  - Exercises: identifying population/sample and parameter/statistic
- Variables and Constants
  - Definitions (domain sets and unresolved entities vs. fixed values)
  - Hierarchy of variable types
    - Qualitative (Categorical): Nominal vs. Ordinal
    - Quantitative (Numerical): Discrete vs. Continuous
  - Levels of Measurement
    - Order, equal intervals, and true zero vs. arbitrary zero
    - Nominal, Ordinal, Interval, and Ratio scales
  - Dimensionality and Time Structure
    - Univariate, Bivariate, and Multivariate data
    - Cross-sectional vs. Time-series data
  - Exercises: classifying variables and measurement levels
- Data Organization, Quality, and Collection
  - Data, data set, element, and observation
  - Tabular representation (features/attributes vs. instances/tuples)
  - Data quality issues (missing values, inconsistent values, duplicates, unit mismatches)
  - Data collection sources (published sources, experiments, surveys, observations)
  - Primary, secondary, and synthetic (pseudo-primary) data
- Tabulation and Frequency Distributions
  - Raw data, arrays (sorted data), and range
  - Properties of a good statistical table; simple vs. two-way tables
  - Ungrouped vs. grouped frequency distributions (with worked table-reading exercises)
  - Class limits, class boundaries, class width ($c$), and class marks
  - Left-end convention and integer-limit vs. continuous intervals
  - Choosing the number of classes ($k$): Square Root Rule vs. Sturges' Rule

## Detailed Notes

### 1. Recap of Class 1 (Population, Sample, Parameters, Statistics)
- **Population vs. Sample**: A population is the entire universe of discourse containing all items of interest. Analyzing an entire population is often impractical because:
  1. **Computational/machine constraints**: Machines lack the capacity to process massive population-scale data directly.
  2. **Loss of detail**: A population contains many ups and downs across diverse characteristics; working at the overall population level makes it hard to track which characteristic belongs to which subgroup. Working with smaller groups (samples or clusters) is necessary for detailed analysis.
- **Generalizability Trade-off**: If a sample accidentally captures only one homogeneous region of the population, results cannot be generalized back to the population.
- **Analogy (Tree Trunk and Furniture)**: A carpenter cuts a tree trunk to build a bench, producing wood wastage. Once the bench is built, you cannot backtrack from the bench to reconstruct the exact original tree trunk because material was lost. Likewise, after sampling and computing statistics, you cannot reconstruct exact population values; you must accept approximate results and account for the loss via **error calculation**.
- **References to Class 1 Material**:
  - The teacher referenced a previously shown table of standard metrics and their symbols comparing **parameters** (population measurements, e.g., population mean $\mu$) and **statistics** (sample measurements, e.g., sample mean $\bar{x}$, where the $x$'s are sample values). The teacher noted that the subject "Statistics" takes its name from sample-level statistics.
  - The teacher also briefly recapped **sampling error**, **non-sampling error**, and **biases** covered earlier, as well as a previously worked example from the last class.

### 2. Sampling Approaches
Because statistical analysis usually operates on samples rather than the full population, data can be sampled using different methods:

1. **Random Sampling**:
   - The most popular and widely accepted method worldwide because it minimizes selection bias (the sampler selects without prior knowledge or preference).
   - **Sampling Frame**: Before sampling, you define a sampling frame specifying the fixed sample size to draw each time (e.g., from 100,000 items, choosing 100 items per sample so every sample has size 100).
   - **Advantages**: Requires little prior knowledge of the entire population; free from selection bias.
   - **Disadvantages / Limitations**:
     - Requires a complete/complex sampling frame, and choosing the right sample size (e.g., whether 100, 200, 500, or 50 out of 100,000 is sufficient) is not predefined. It depends on the analyst's domain expertise and experimentation.
     - Pure randomness can still accidentally cluster in one area and miss other groups (analogy: closing your eyes and pointing repeatedly may hit the same region while leaving others out).

2. **Systematic Sampling**:
   - After a random start, every $k$-th member of the sampling frame is chosen (e.g., picking every 3rd element across rows or columns).
   - Well suited for data with fixed intervals, spatial distances, or time-series ordering.

3. **Stratified Sampling**:
   - The population is divided into distinct groups called **strata** (singular: stratum; the teacher emphasized that "stratified" is a term students will encounter repeatedly in future courses).
   - A random sample is then drawn from *each* stratum, ensuring representation across all groups.

4. **Cluster Sampling**:
   - Subsets of data are grouped into **clusters**, and entire clusters are selected as samples for observation (rather than picking a few items from every group).

- **Choosing a Method**: No single method fits every dataset. The choice depends on the nature of the data (numerical vs. categorical, continuous vs. discrete, nominal vs. ordinal, time-series vs. grouped vs. unstructured).

#### Worked Exercise: Population/Sample and Parameter/Statistic
1. *"The load times of 500 randomly selected page requests have mean 1.8 seconds."*
   - **Scope**: Sample (500 out of an unlimited number of page requests).
   - **Metric / Symbol**: Statistic, sample mean $\bar{x}$.
2. *"In a random sample of 200 RUET students, 64% use Linux."*
   - **Scope**: Sample (200 students).
   - **Metric**: Statistic, sample proportion/percentage ($64\%$).
3. *"The mean CGPA of all 180 third-year CSE students computed from the department's record..."*
   - **Scope**: Population. Always check the **domain** (universe) first: since all 180 third-year CSE students make up the entire universe for that group, no subset was taken.
   - **Metric / Symbol**: Parameter, population mean $\mu$.

### 3. Variables and Constants
- **Variable**: A symbol (such as $x$, $h$, $n$) representing an undetermined or unresolved entity that accepts values from a given prior **domain set** (a set containing a range of allowed values). Substituting a value from the domain resolves the variable.
- **Constant**: An entity that can assume only one fixed value; it cannot be changed or altered.
- **Example**: Among third-year students, CGPA varies from student to student (**variable**), whereas the year of study ("3rd year") stays fixed (**constant**).

### 4. Types of Variables and Levels of Measurement
Variables are divided into two broad categories:

```
Variables
├── Qualitative (Categorical)
│   ├── Nominal
│   └── Ordinal
└── Quantitative (Numerical)
    ├── Discrete
    └── Continuous
```

- **Qualitative (Categorical) Variables**: Represented by labels or categories rather than numeric measurements (e.g., milk is "good" or "bad"; weather is "sunny" or "rainy").
  - **Nominal**: Named categories with established conventions/labels and no inherent order (e.g., blood groups $O+$, $A$, $B$; operating systems Linux, Windows).
  - **Ordinal**: Categories that have a natural **sequence, order, or ranking**, without standardized universal spacing (e.g., satisfaction ratings: bad, intermediate/satisfactory, good, fair, best, excellent; letter grades: $F, D, C, B, A, A+$, where different institutions define different scales such as $B-$, $C-$, or tiers above $A+$).
- **Quantitative (Numerical) Variables**: Measurable quantities represented by numbers (e.g., 5 liters of milk, 1 kg, 2 rooms).
  - **Discrete**: Values that are distinct, typically finite, and **countable**. Note from the teacher: discrete usually uses integers, *not* because decimals are forbidden, but because values come from a countable, distinct set. For example, $\{0.25, 1.25, 2.25, 3.25\}$ is still discrete (4 countable decimal values), whereas integers alone are only a partial description. Examples: number of children, packets dropped.
  - **Continuous**: Values that are uncountable and unbounded (infinitely many possible values; e.g., taking decimals between 1 and 2 yields infinitely many values). Examples: height of a tree, time.

#### Levels of Measurement
Measurement levels are classified by three criteria: **Order**, **Equal Intervals**, and **True Zero**:

| Level | Data Type | Order | Equal Intervals | True Zero |
| :--- | :--- | :---: | :---: | :---: |
| **Nominal** | Qualitative | No | No | No |
| **Ordinal** | Qualitative | Yes | No | No |
| **Interval** | Quantitative | Yes | Yes | No (Arbitrary zero) |
| **Ratio** | Quantitative | Yes | Yes | Yes |

- **True Zero vs. Arbitrary Zero**:
  - **True Zero**: Zero means complete absence ("nothing" / no quantity exists), and ratios are physically meaningful.
    - *Examples*: Kelvin temperature ($0\text{ K}$ means no thermal energy; $200\text{ K} / 100\text{ K} = 2$ and $50\text{ K} / 25\text{ K} = 2$), weight ($0\text{ kg}$ = no weight), time ($0\text{ ms}$ = no duration).
  - **Arbitrary Zero**: Zero is just a chosen reference point on a scale and still carries meaning; negative values can exist, and ratios do not hold.
    - *Example 1 (Celsius)*: $0^\circ\text{C}$ does not mean "no temperature" (temperatures can go down to $-273^\circ\text{C}$, i.e., $0\text{ K} \approx -273^\circ\text{C}$). Moreover, $20^\circ\text{C} / 10^\circ\text{C} = 2$, but in Kelvin that is $293\text{ K} / 283\text{ K} \neq 2$, so Celsius is an **interval** scale, not ratio.
    - *Example 2 ($\text{pH}$ scale)*: $\text{pH } 3$ is not half or double $\text{pH } 6$; ratios do not apply, so $\text{pH}$ requires an **interval** scale.

#### Dimensionality and Time Structure
- **Based on Number of Variables**:
  - **Univariate**: 1 variable (e.g., student weights, or CGPA, or names).
  - **Bivariate**: 2 variables (e.g., student name and CGPA; student name and roll).
  - **Multivariate**: More than 2 variables (increases analytical complexity/degree).
- **Cross-Sectional vs. Time-Series Data**:
  - **Cross-Sectional Data**: Data observed on many elements at the *same* point in time (e.g., collecting data right now from all 60 students in the room).
  - **Time-Series Data**: Data observed on a single element across successive points over a time interval (e.g., picking one student today and measuring a metric across the entire semester).

#### Worked Exercise: Classifying Variables
1. *Residence hall of each student in a class*: **Qualitative, Nominal** (hall names have no order).
2. *Petrol pumped by the next 10 customers*: **Quantitative, Continuous, Ratio** (any continuous volume can be pumped; $0$ liters means no petrol).
3. *HTTP status code of a request ($200, 404, 500$)*: **Qualitative** (even though numeric in appearance, these are labels/identifiers for status names, not measurable quantities).
4. *Number of retries before a request succeeds*: **Quantitative, Discrete, Ratio** (finite/countable integer attempts in practice; $0$ retries means no retry needed).
5. *App rating from 1 to 5 stars*: **Qualitative, Ordinal** (ordered rating levels).
6. *Time taken to finish a homework assignment*: **Quantitative, Continuous**.

### 5. Data Organization, Quality, and Collection
- **Core Definitions**:
  - **Data**: Raw facts existing in nature without inherent meaning. Data must be shaped/reformed to become **information**.
  - **Data Set**: A raw collection of data brought together (e.g., gathered into a common container) prior to processing. A data set with $n$ elements and $k$ variables contains $n \times k$ data items.
  - **Element**: The entity on which data is collected (e.g., "Age" when recording values like $10, 15, 20, 25, 30$ for a class).
  - **Observation**: The set of domain values recorded for an element.
- **Tabular Structure**:
  - Connecting to the Database course taught in the same semester: columns are **attributes** (called **features** in statistics/ML), and rows are **tuples** (called **instances** in statistics/ML, representing observations at each entity/timestamp).
- **Data Quality Issues** (demonstrated on a sample request-log table):
  - **Missing values**: Empty/unrecorded entries (e.g., missing size in row 3 due to lack of resources or recording failure). Must be **imputed** or, if imputation is impossible, the row must be dropped.
  - **Inconsistent / impossible values**: E.g., time $= -610\text{ ms}$, which cannot happen physically. Must be removed or fixed.
  - **Duplicacy**: Identical rows repeated (e.g., `R2, 404, 21.6` appearing twice). Large-scale duplication (e.g., 50,000 duplicates in 100,000 rows) distorts results and wastes computation time; duplicates must be removed before analysis.
  - **Unit / formatting errors**: Unwanted values or mismatched units appearing inside a column defined for a specific unit (e.g., milliseconds).
- **Data Collection Sources**:
  - **Published sources**: E.g., Census reports and statistics from the Bangladesh Bureau of Statistics (BBS).
  - **Designed experiments**, **surveys**, and **observational studies / regular monitoring** (e.g., tracking car tire punctures or fueling failures over time to identify causes).
  - *Note on online repositories*: Platforms like Kaggle (and Google Scholar for papers) are aggregators/collections of sources rather than primary original sources themselves.
- **Primary vs. Secondary Data**:
  - **Primary Data**: Collected directly by the experimenter/observer. Often higher quality for the task, but collection is lengthy, complex, and requires verification and authorization.
  - **Secondary Data**: Data already collected by someone else and reused by the analyst (common for smaller/faster studies).
  - **Synthetic (Pseudo-Primary) Data**: Generated data used when neither primary nor secondary data is available.

### 6. Tabulation and Frequency Distributions
- **Raw Data, Array, and Range**:
  - **Raw Data**: Unorganized, unsorted collected data without structure.
  - **Array**: In statistics, raw data arranged in ascending or descending numeric order (different from a programming array, as sorting is required here).
  - **Range**: Computed after sorting into an array:
    $$\text{Range} = \text{Largest value} - \text{Smallest value}$$
- **Characteristics of a Good Table**:
  1. Clear table number and title.
  2. Short column/row headings with units.
  3. Rows arranged in a logical order.
  4. Related figures (numeric values) placed side by side.
  5. Data source cited in a footnote.
- **Simple vs. Two-Way Table**:
  - **Simple Table**: Summarizes data against a single criterion/variable (e.g., count of CSE students).
  - **Two-Way Table**: Summarizes data across two or more criteria/directions (e.g., department [CSE, EEE] vs. OS usage [Mac OS %] along with totals).

#### Ungrouped vs. Grouped Frequency Distributions
- **Ungrouped Frequency Distribution**: Lists the frequency of every distinct value individually, preserving exact individual counts.
  - *Worked Example 1 (Sick Leave)*: Days of sick leave ($0$ to $9$) taken by $50$ workers over $6$ weeks:
    - At least 1 day of sick leave: $50 - \text{freq}(0) = 50 - 12 = 38$.
    - From 3 to 5 days (inclusive): $\text{freq}(3) + \text{freq}(4) + \text{freq}(5) = 17$ (8 + 5 + 4, or similar; sum of 3, 4, 5 frequencies gave 17, and $5 + 9$ etc. from the board). Note: if *exclusive*, boundary values are omitted.
    - More than 5 days: sum frequencies for $6, 7, 8, 9$ (excluding $5$).
  - *Worked Example 2 (Items Sold, Total $= 42$)*:
    - At least 2 sold: $42 - (\text{freq}(0) + \text{freq}(1)) = 42 - 9 = 33$.
    - At least 5 sold: sum frequencies from $5$ upward.
    - Even number sold: sum frequencies for $0, 2, 4, 6$ (note that $0$ is included as an even number).
- **Grouped Frequency Distribution**: Groups data into class intervals (e.g., $60\text{--}62$, $63\text{--}65$, $66\text{--}68$, $69\text{--}71$).
  - **Trade-off**: Individual values are hidden (e.g., knowing 5 students fall in $60\text{--}62$ does not tell you how many scored exactly $61$), but it reveals the overall data pattern and keeps large datasets manageable.

#### Class Terminology, Boundaries, and Conventions
Consider the non-overlapping classes $60\text{--}62$, $63\text{--}65$, $66\text{--}68$, $69\text{--}71$:
- **Class Limits**: Left number is the **lower limit** ($60$), right number is the **upper limit** ($62$).
- **Class Boundaries**: Because there is a gap between $62$ and $63$, continuous values like $62.3$, $62.4$, $62.8$, or $62.9$ need a clear boundary.
  - In large real-life datasets, a $0.05$ adjustment may be used; in small/classroom examples, we adjust by $\pm 0.5$:
    - Lower class boundary $= 60 - 0.5 = 59.5$
    - Upper class boundary $= 62 + 0.5 = 62.5$
- **Class Width ($c$)**: Difference between upper and lower class boundaries (here $62.5 - 59.5 = 3$).
- **Class Mark**: The midpoint of a class, e.g., $(60 + 62)/2 = 61$. For grouped calculations, every observation in the class is approximated by the class mark (acknowledging some deviation/error around it).
- **Integer-Limit vs. Continuous Intervals & Left-End Convention**:
  - Non-overlapping intervals ($60\text{--}62$, $63\text{--}65$) are called **integer-limit intervals**.
  - Overlapping intervals ($60\text{--}62$, $62\text{--}64$, $64\text{--}66$) are called **continuous intervals**, where limits and boundaries coincide.
  - To prevent ambiguity on shared endpoints (e.g., where does $62$ go between $60\text{--}62$ and $62\text{--}64$?), we use the **left-end convention**: each interval $[a, b)$ includes its left (lower) endpoint $a$ and excludes its right (upper) endpoint $b$. Thus $60$ to $61.99$ stays in $60\text{--}62$, while $62$ goes into the next class $62\text{--}64$ ($62 \le x < 64$).

#### Determining the Number of Classes ($k$)
- **Standard Guideline**: Keep the number of classes $k$ between **$5$ and $20$**.
  - Too few classes hide the shape of the distribution (cramming too much data together).
  - Too many classes leave many intervals nearly empty, making analysis unreliable.
- **Two Rules for Choosing $k$** (where $n$ is the number of data points):
  1. **Square Root Rule** (rule of thumb / basic approach):
     $$k \approx \sqrt{n}$$
  2. **Sturges' Rule** (most commonly used):
     $$k \approx 1 + 3.322 \log_{10}(n)$$
- **Comparison Across Sample Sizes ($n$)** (from the teacher's board/slide table):
  - $n = 40$: $\sqrt{n} = 6.3$ (choose $6$ or $7$); Sturges $= 6.3$ (round up to $7$). Both match.
  - $n = 100$: $\sqrt{n} = 10$ (use $10$); Sturges $= 7.6$ (round up to $8$).
  - $n = 500$: $\sqrt{n} = 22$ (exceeds $20$, so cut/cap at $20$); Sturges $= 10$ (cleanly within $5$ to $20$).
  - $n = 1000$: $\sqrt{n} = 32$ (exceeds $20$, must cap at $20$); Sturges stays within $20$, giving a precise class count without manual capping.

## Exam / Important Points
- **"Stratified"**: Highlighted as a key concept you will encounter in several future courses.
- **Always identify the domain first** when deciding between population (parameter) and sample (statistic). For example, "180 third-year CSE students" is a population in the context of RUET 3rd-year CSE, not a sample.
- **Discrete vs. Integer trap**: Discrete means distinct and countable, *not* strictly integer-only (a finite set of decimals like $\{0.25, 1.25, 2.25\}$ is still discrete).
- **Zero is an even number**: Remember to include $0$ when asked for "even numbers" in frequency-table counting problems.
- **Inclusive vs. Exclusive ranges**: Pay close attention to wording like "from 3 to 5 (inclusive)" vs. "more than 5" (excludes 5).
- **Numbers used as labels**: Numeric codes like HTTP status codes ($200, 404, 500$) are **qualitative**, not quantitative.
- **True zero vs. Arbitrary zero**: Know why Kelvin ($0\text{ K}$) is a ratio scale while Celsius ($0^\circ\text{C}$) and $\text{pH}$ are interval scales.
- **Left-end convention**: Know how to resolve values falling directly on continuous interval boundaries ($[a, b)$).
- **Sturges' Rule vs. Square Root Rule**: Know both formulas and why Sturges' rule is preferred for larger $n$ (stays within $5\text{ to }20$).

## Announcements & Logistics
None mentioned.

## Open Questions / Unclear Parts
- **~17:15, ~47:00, ~56:00**: Student answers during class Q&A were off-mic/quiet, though the teacher repeated or clarified the key conclusions each time.
- **~1:01:00**: When writing the continuous interval inequality for $62\text{--}64$, the teacher briefly misspoke ("$x \le 62$, sorry, wrote it backwards") before immediately clarifying that the right endpoint is exclusive ($62 \le x < 64$) so that $62$ moves to the next class.
- **~1:04:30**: For the "items sold (total 42)" ungrouped table exercise, the full frequency table on the slide was not read aloud row by row (only specific counts such as $9$ for $0$ and $1$ combined, and the final answers, were spoken).
- **~1:08:20**: For $n = 1000$ in the comparison table, the teacher stated that Sturges' rule gives a value within $20$ without reading the exact computed number aloud.
