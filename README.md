# What Should We Actually Write About?

Dataquest guided project, *Popular Data Science Questions*. Dataset: Data Science Stack Exchange questions, 8,839 from 2019 with engagement metrics plus 21,576 spanning 2014-05 to 2020-01.

## The claim I checked

The conclusion normally drawn from this dataset is that **deep learning is the most popular topic right now**, reached by ranking tags on view counts.

Two things make that ranking unsafe, and both are measurable here.

## Findings

### 1. Views measure age as much as interest

| Posted | Mean views |
|---|---|
| January 2019 | 314.5 |
| December 2019 | 33.1 |

**A January question averages 9.5 times the views of a December one**, on a site where question volume was *rising* across the year (573 in January, 731 in December). Correlation between day-of-year and log views: **-0.40**. This is accumulated exposure, not a change in activity.

Any tag whose use grew during 2019 is penalised by this metric; any tag that faded is flattered.

### 2. Total views rewards volume, not interest

Ranking each question against those posted in the same month removes the age effect. The headline tags land at dead centre:

| Tag | Questions | Median view percentile | Engagement rank |
|---|---|---|---|
| deep-learning | 1,220 | **0.497** | 51 of 89 |
| machine-learning | 2,693 | **0.500** | 50 of 89 |
| neural-network | 1,055 | 0.509 | - |

**A deep learning question is, to three decimals, the median question on the site.** It collects 233,628 views because 1,220 questions carry the tag, not because any of them drew a crowd. Total views is volume multiplied by interest, and with interest at average, volume alone decides the ranking.

The tags that genuinely over-perform are specific and practical, and none appears near the top of the standard ranking:

| Tag | Questions | Median view percentile |
|---|---|---|
| bert | 64 | 0.778 |
| dataframe | 81 | 0.761 |
| class-imbalance | 73 | 0.734 |
| xgboost | 165 | 0.691 |
| pandas | 354 | 0.678 |
| overfitting | 69 | 0.657 |

### 3. Tags are not topics

`deep-learning`, `neural-network`, `keras`, `tensorflow`, `cnn`, `lstm` and `pytorch` all describe one area, and **58.4% of deep-learning questions carry at least one of the others**. Counting the union instead of the pieces, the family touches **35.4% of all 2019 questions**, against the 13.8% the single tag suggests.

### 4. The growth story ended before the data did

| Period | Deep learning share |
|---|---|
| 2014Q2 | 4.5% |
| 2016Q4 | 27.1% |
| 2017Q4 | 33.5% |
| **2018Q3** | **41.3% (peak)** |
| 2019Q1 to Q4 | 35.8%, 35.4%, 34.5%, 35.9% |

Deep learning grew ninefold as a share of the site between 2014 and 2018, then went flat for six straight quarters. "Most popular right now" is true. "The topic to bet on" does not follow, and a view-count ranking cannot tell the two apart.

Meanwhile `bert` appears from nothing in 2019 (6, 21, 8, 29 questions by quarter) and tops the corrected engagement ranking. Small, new and over-performing is what a growth opportunity looks like here.

## Recommendation

Do not commission a deep learning series on the strength of its view counts. Write deep learning content because a third of the audience is already there, and write the specific practical pieces (BERT, dataframe manipulation, class imbalance, xgboost, overfitting, cross-validation) because they are what people actually read.

## Method

1. Parse `<a><b>` tag strings into lists.
2. Rank each question by views *within its posting month*, giving a percentile that is free of the age effect.
3. Summarise per tag with a 60-question floor, leaving 89 tags.
4. Compare that ranking against the naive total-views one.
5. Aggregate related tags into topic families, and track family share per quarter across the six-year file.

## What I would not claim

- **Views are a weak proxy for what we care about.** Readers of a tutorial are not askers of a question, and heavy views may mean the documentation is bad rather than the topic interesting.
- **The percentile correction handles age, not everything else.** Google indexing and inbound links drive views too, and neither is in this file.
- **The 60-question floor is a judgement call.** Lowering it admits noisier tags; raising it would drop `bert` (64 questions) and hide the most interesting finding.
- **bert rests on 64 questions.** A real signal but a thin one. I would want 2020 data before committing a budget.
- **The deep learning family is my grouping,** nine tags chosen by hand. A different grouping shifts 35.4% but not the plateau.
- **This is one Stack Exchange site,** skewed toward practitioners debugging code. It is not a survey of the field.

## Files

- `notebook.ipynb`: full analysis, executed, with three charts.

## Stack

pandas, NumPy, Matplotlib (fivethirtyeight style). No seaborn.