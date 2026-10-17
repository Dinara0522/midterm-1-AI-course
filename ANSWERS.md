# Midterm 1: answers

**GitHub username: Dinara0522**

**Session code: MAPLE-66**

**Fingerprint: 3841b484**

## AI-use declaration
I used ChatGPT to help interpret the exam instructions, organize the solution, check the calculation methods, and draft explanations of the results. I used Google Colab to run the provided data-generation notebook and obtain my individual exam data. I used the generated DATA.md and CSV files as the source of the values used in Parts 1, 2, and 3. ChatGPT helped me check retrieval metrics, 95% Wilson intervals, annual cost calculations, document-pipeline accuracy, and the reasoning behind my decisions. I also used GitHub to maintain and submit my ANSWERS.md file. AI assistance was used for analysis and writing support, not as a substitute for understanding the results. I am responsible for reviewing the calculations, checking that they match my generated data, and being able to explain the methods, assumptions, and trade-offs during the oral check.


## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A |0.6833|0.8167|0.9000|0.7632|
| B |0.2333|0.4500|0.7167|0.3895|

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 |0.8167|0.7008|0.8944|
| A, k=5 |0.9000|0.7985|0.9534|
| B, k=3 |0.4500|0.3309|0.5751|
| B, k=5 |0.7167|0.5923|0.8149|

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 |17169.38|
| A, k=5 |22559.41|
| B, k=3 |11381.38|
| B, k=5 |12912.73|

### 1d. Decision

Chosen candidate: B, k=5

I chose B, k=5 because its annual cost is $12,912.73, within the $15,000 budget. Its recall@5 is 70% for EN (14/20), 75% for RU (15/20), and 70% for KK (14/20). EN and KK are the weakest-served languages. Configurations A exceed the annual budget. The Wilson intervals for B, k=3 and B, k=5 do not overlap, supporting B, k=5 under the course's comparison rule.


### 1e. Next measurement
Evaluate A, k=3 and B, k=5 on a larger independently labelled test set, with at least 100 questions per language. Compare per-language recall and 95% Wilson intervals to check whether the observed differences persist and whether the budget-feasible choice remains adequate.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H |0.8833|KK, degraded|0.7333|0.5555|0.8582|14907.51|
| L |0.8056|KK, degraded|0.6333|0.4551|0.7813|18000|

Personal-data pages per year sent abroad under H: 1023825

### 2b. Memo
I recommend Pipeline L, subject to a local security and performance acceptance test. H has higher overall accuracy (88.3% versus 80.6%) and lower annual cost ($14,907.51 versus $18,000). However, both pipelines perform worst on degraded Kazakh invoices. H gets 22/30 correct (73.3%; 95% Wilson interval 55.6–85.8%), while L gets 19/30 (63.3%; interval 45.5–78.1%). These intervals are wide, and overall averages hide poorer performance on degraded Kazakh documents.

Under H, approximately 1,023,825 pages containing a name and ИИН would leave Kazakhstan annually. Kazakhstan's personal-data law covers ИИН. Before using H, we must establish where processing occurs, who stores scans and extracted JSON, and how long both are retained. A vendor's statement alone is not a compliance review. For L, processing stays on the bank's server, but we must still verify administrator access, logs, backups, and deletion practices.

Safeguards should include role-based access, encryption in transit and at rest, restricted logging of personal data, tested deletion and retention rules, and a documented audit of data flows. We should measure accuracy by language and scan condition before deployment. L reduces cross-border exposure but costs $3,092.49 more per year and has lower measured accuracy. Its residual risk is extraction error, especially on degraded Kazakh documents; uncertain fields should be sent for human review.

## Part 3: Explain your own numbers

### Q1

Number: 2.73

Why: The bill ratio differs from the total-token ratio because input and output tokens have different prices. Output tokens cost six times as much as input tokens, and the two languages have different input/output mixes.


### Q2

Number: 355

Why: Scaling gives 576 × 263/256 ≈ 592 e5 tokens; 60% is about 355. The sentence starts before the 512-token limit and is short enough to fit, so it can be included. Truncation beyond the limit may be silent.

### Q3

Number: 45.5%

Why: Increasing temperature softens the probability distribution without changing the ranking of these tokens. All five tokens still have nonzero sampling probability; temperature changes their relative probabilities, not the candidate set.

### Q4

Number: 30.4%

Why: I excluded arithmetic sequences and multiplication because their answers can be derived algorithmically. The birthday and synthetic account-number sets contain one-off facts. A system prompt cannot supply missing factual knowledge or guarantee correct recall.

### Q5

Number: 4.25

Why: The model has about 85 tokens per parameter, compared with Chinchilla's 20. By this criterion it is over-trained in tokens relative to its parameter count. Chinchilla argued that models such as GPT-3 were under-trained and could use more training tokens for their size.
