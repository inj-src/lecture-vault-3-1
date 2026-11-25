---
course: "CSE 3109 – Applied Statistics and Queuing Theory (ASQT)"
class: "ASQT - 1"
duration: "32:02"
---
# ASQT - 1 – Course Introduction & Fundamentals of Statistics

## Overview
This first lecture of CSE 3109 (Applied Statistics and Queuing Theory) introduces the course syllabus, Course Outcomes (COs) and updated Program Outcomes (POs), and the foundational concepts of statistics. The teacher covers what statistics is, the stages of a statistical study, descriptive vs. inferential statistics, real-world and CS applications, population vs. sample (parameters vs. statistics), and sampling vs. non-sampling errors. This lays the groundwork for the rest of the course, which progresses through statistical measures, probability, probability distributions, hypothesis testing, and queuing theory.

## Topic Map
- Course Introduction & OBE Structure
  - Syllabus overview (dispersion, correlation, causality, hypothesis testing, probability, distributions, queuing theory)
  - Prerequisites (permutations/combinations from Discrete Mathematics; integration & differentiation)
  - 3 Course Outcomes (CO1: Apply, CO2: Analyze, CO3: Evaluate)
  - Updated 12 Program Outcomes (POs) & mapping to PO1, PO2, PO4
- Introduction to Statistics
  - Definition & purpose (explainability, decision-making, prediction)
  - Multiple meanings of "statistics" (methods, raw data lists, sample-derived numbers)
  - Stages of a statistical study (5-step pipeline)
- Branches of Statistics
  - Descriptive Statistics (Descriptive Analysis)
  - Inferential Statistics (Predictive Analysis)
- Applications of Statistics
  - Business/retail, engineering, health, government, weather/disaster forecasting
  - CS applications (performance evaluation, computer networks, machine learning, software engineering)
- Population, Sample, Parameters & Statistics
  - Population (Finite vs. Infinite) & Census
  - Sample & Sampling Frame
  - Advantages and trade-offs of sampling vs. population/census
  - Variable, Parameter vs. Statistic (symbols & comparison)
  - Worked example (faculty ages)
- Errors in Statistical Studies
  - Sampling Error (and effect of sample size)
  - Non-Sampling Errors (Selection Bias, Non-Response Bias, Response Bias)

## Detailed Notes

### 1. Course Overview, Prerequisites & OBE Mapping
- **Syllabus Topics Mentioned**:
  - Measures of dispersion, correlation theory, causality (cause-and-effect) analysis.
  - Tests of significance (hypotheses and hypothesis testing).
  - Major portion: Probability, probability-oriented topics, and probability distributions.
  - Queuing theory (final portion).
- **Mathematical Prerequisites**:
  - Probability builds on permutations and combinations (*বিন্যাস ও সমাবেশ* — *binnash o shomabesh*), previously covered in Discrete Mathematics.
  - Some formulas (such as central tendency measurements) will be derived using integration and differentiation.
- **Course Outcomes (COs)** (organized by Bloom's taxonomy cognitive levels rather than topic chunks):
  - **CO1 (Apply)**: Introductory concepts; applied (*প্রয়োগমূলক*) questions where known formulas are applied to given data.
  - **CO2 (Analyze)**: Mid-level concepts; given data or results, analyze whether they fit a particular topic/method, diagnose issues, and re-correct if needed.
  - **CO3 (Evaluate)**: Complex engineering/scenario-based or real-world problems requiring analysis, applying formulas, and evaluating an overall solution.
- **Updated OBE / PO Mapping**:
  - The department is transitioning to an updated version of Outcome-Based Education (OBE) for future BAETE accreditation.
  - Key change in the 12 Program Outcomes (POs): old PO6 (Engineering & Society) and old PO7 (Environment & Sustainability) were merged into PO6; subsequent POs shifted down by one index (old PO12 Lifelong Learning became PO11); a new **PO12 (Entrepreneurship)** was added.
  - This course maps to **3 POs**:
    - **PO1** (Engineering Knowledge) $\rightarrow$ aligns with CO1 (Apply)
    - **PO2** (Problem Analysis) $\rightarrow$ aligns with CO2 (Analyze)
    - **PO4** (Investigation) $\rightarrow$ aligns with CO3 (Evaluate)
  - Class tests, assignments, and semester finals will be designed around these COs and rubrics.

### 2. Introduction to Statistics: Meaning & Stages
- **Bengali Term**: পরিসংখ্যান (*Porishongkhan*).
- **Why We Need Statistics** (from class discussion):
  - Converting raw data into useful information.
  - Observing data to take actions and make predictions.
  - **Data Explainability** (emphasized by the teacher as the primary need): explaining how data looks, how it behaves, and what its characteristics are through statistical measurements.
- **Formal Definition**:
  - Scientific methods, approaches, or techniques used for:
    1. **Collecting** data
    2. **Organizing** data (arranging it in a structured way to reveal behavior and characteristics)
    3. **Summarizing** data
    4. **Presenting** data
    5. **Analyzing** data
  - Purpose: To draw **valid conclusions** and make **reasonable decisions**. The teacher described this sequence as a **pipeline** rather than just a cycle.
- **Other Meanings of the Term "Statistics"**:
  1. **The data themselves**: A collection/list of numerical facts (e.g., environmental statistics, employment statistics, accident statistics).
  2. **A statistic (singular)**: A numerical value computed from a sample (such as a sample average).
- **Stages of a Statistical Study**:
  1. Design research questions (identify which data needs to be investigated).
  2. Collect data (via surveys, experiments, or published records).
  3. Present data (tables, charts, graphs, bar plots, etc.).
  4. Analyze the data.
  5. Draw conclusions.

### 3. Descriptive vs. Inferential Statistics
Statistics is divided into two main branches (also referred to as **Descriptive Analysis** and **Predictive Analysis**):
1. **Descriptive Statistics**:
   - Focuses on summarizing and explaining data using tools such as tables, graphs, and summary measures.
2. **Inferential Statistics (Predictive Statistics)**:
   - Uses sample summaries to deduce/estimate results about a broader dataset, design and test hypotheses, and reach conclusions/predictions.

- **Population–Sample–Inference Workflow** (explained from a slide diagram):
  ```
  [ Population ]  ---( Sampling )--->  [ Sample ]
        ^                                   |
        |                                (Analysis)
   (Inference /                             v
    Prediction) <--------------------- [ Sample Results ]
  ```
  - Because the full population may be huge or uncountable, a smaller, countable subset (**sample**) is drawn, analyzed, and its results are used to predict/infer properties of the original population (assuming shared characteristics).

### 4. Applications of Statistics
- **General Domains**: Business and industry, engineering, health, government, environmental/weather forecasting, and earthquake prediction.
- **Real-World Retail Example (Market Research & Data Orientation)**:
  - Supermarkets and showrooms analyze customer purchasing history/behavior to organize store layouts—placing related items together (e.g., lentils next to rice, fruits next to vegetables, rather than at opposite corners) and reshuffling layouts every 2–3 months based on purchasing patterns.
- **Computer Science & Engineering Applications**:
  - **Performance Evaluation**: Used across CS courses (at minimum, calculating the **mean/average**).
  - **Computer Networks**: Analyzing packet delivery (covered in later semesters).
  - **Machine Learning**: Heavily grounded in statistical methods.
  - **Software Engineering**.

### 5. Population, Sample, Parameters & Statistics
- **Variable**: A characteristic recorded for each member/element of a study (the attribute being measured).
- **Population**:
  - The entire collection of individuals or objects about which information is desired (analogous to the *universal set* / "universe of discourse" in Set Theory).
  - What counts as the population depends on the study's scope (e.g., all humans in the world, citizens of Bangladesh, all RUET students, the CSE department, or just a single class section).
  - **Types of Populations**:
    - **Finite Population**: Countable and bounded within a range/territory (e.g., CSE students of RUET).
    - **Infinite Population**: Uncountable with infinitely many possible observations (e.g., all possible outcomes of successively tossing a coin indefinitely).
- **Census**: A study that observes every single member of the population.
- **Sample**:
  - A subset of the population selected using a defined ratio, rate, or sampling frame (e.g., selecting one section of ~50 students out of ~900 CSE department students).
  - The same group can act as a **population** in one context and a **sample** in another depending on the problem definition.
- **Advantages & Trade-offs of Sampling** *(note: the teacher verbally said "census" when introducing the slide on advantages, but the points discussed—lesser time, lower cost, working with a subset of the population—are the advantages of **sampling** over a census)*:
  - **Advantages**:
    - Takes less time and lower cost (requires lower computational power/hardware).
    - Produces results with sufficient precision.
    - Avoids destroying every item when testing is destructive ("testing may destroy the item").
    - In massive populations, individual data points or outliers can get lost/overlooked; in a curated sample, every selected data point is tracked and included in the analysis.
  - **Trade-offs / Disadvantages**:
    - Informative data points or crucial features might be missed during sampling, affecting feature/characteristic analysis (mitigation techniques will be taught later).
- **Parameter vs. Statistic**:
  - **Parameter**: A numerical measurement describing a **population**. Generally fixed (for a finite population) and often unknown.
  - **Statistic**: A numerical measurement describing a **sample**. Values are known because they are computed directly from the observed sample.

| Measurement | Population (Parameter) | Sample (Statistic) |
| :--- | :---: | :---: |
| Size | $N$ | $n$ |
| Mean | $\mu$ | $\bar{x}$ |
| Standard Deviation | $\sigma$ | $s$ |
| Proportion | $p$ | $\hat{p}$ |

- **Worked Example (Faculty Age)**:
  - *Problem*: A Dean records the ages of 10 faculty members in order to estimate the average age of all faculty members. Identify the variable, population, sample, parameter, and statistic.
  - **Variable**: Age
  - **Population**: All faculty members
  - **Sample**: The 10 recorded faculty members
  - **Parameter**: Mean (average) age of all faculty members
  - **Statistic**: Mean (average) age of the 10 sampled faculty members

### 6. Errors in Statistical Studies: Sampling vs. Non-Sampling Errors
To remain neutral and avoid bias when creating a sample, elements are typically chosen randomly. However, errors still arise in two categories:

1. **Sampling Error**:
   - Occurs simply because only a part of the population is observed rather than the whole population. Even with random selection, observations may accidentally cluster in one subgroup/region.
   - *Example*: Choosing 5 students at random to estimate a class's average CGPA—if all 5 happen to have >3.9 or <3.0, the sample mean will differ from the true class mean (or the mean CGPA of 30 students differing from all students).
   - **Behavior with Sample Size**: Sampling error **decreases as the sample size increases** (covering more of the population). However, unless the entire population is studied, some error/bias cannot be completely eliminated, so critical decisions require caution.

2. **Non-Sampling Errors (Biases)**:
   - **Selection Bias**: Some members of the population cannot be selected or are excluded from coverage (e.g., an online survey misses people without internet access).
   - **Non-Response Bias**: Those who do not respond differ systematically from those who do (e.g., only satisfied students returning a feedback form—though the teacher noted humorously that among students here, dissatisfied ones often give more feedback).
   - **Response Bias**: Answers or measurements are systematically wrong due to flawed timing, collection methods, or procedures.

## Exam / Important Points
- **CO-aligned question styles**: Expect CO1 questions to ask for direct formula application to data; CO2 questions to give data/results and ask you to analyze, check fit, or correct them; CO3 questions to present real-world/scenario-based problems requiring full analysis, calculation, and evaluation.
- **Distinguish Parameter vs. Statistic and their symbols**: Carefully keep population symbols ($N, \mu, \sigma, p$) separate from sample symbols ($n, \bar{x}, s, \hat{p}$)—the teacher explicitly warned not to mix them up.
- **Population vs. Sample identification**: Be ready to identify the Variable, Population, Sample, Parameter, and Statistic from a short word problem (like the Dean / faculty age example).
- **Sampling Error vs. Non-Sampling Errors**: Know that sampling error comes from observing only a subset (and decreases as sample size $n$ increases), whereas Selection Bias, Non-Response Bias, and Response Bias are **non-sampling errors**.

## Announcements & Logistics
- **Attendance**: Will be counted starting from the next class.
- **Course Outline & Materials**: The teacher will share the course outline (containing the CO/PO mapping, rubrics, and list of reference books) with the students; students should collect the listed books once shared.
- **Assessments**: Class tests, assignments, and the semester final will be designed based on the 3 Course Outcomes (CO1–CO3) and their rubrics (no specific dates announced yet).

## Open Questions / Unclear Parts
- **00:00**: The recording starts mid-sentence while the teacher is reading earlier syllabus items (just before "measures of dispersion"); the opening few words/topics (likely central tendency) are cut off.
- **00:08–00:15**: The phrase before "analysis" ("causality analysis" / "cause-and-effect analysis") is slightly muffled.
- **04:30–04:55 & 15:25–15:35**: Reference book titles, exact rubric percentages, and full slide wording (e.g., around "testing may destroy the item") were shown on slides rather than read aloud in full.
