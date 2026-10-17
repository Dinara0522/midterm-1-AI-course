# Midterm 1: answers

GitHub username: Dinara0522
Session code: MAPLE-66
Fingerprint: 3841b484

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration
I used ChatGPT as an AI assistant to help interpret the exam instructions, organize calculations, check statistical formulas, and draft explanations. I used the individual data generated for my GitHub username and session code. The calculations cover retrieval metrics, Wilson confidence intervals, annual model costs, document extraction accuracy, and the five conceptual questions. I am responsible for checking the results and understanding the methods and trade-offs in my answers.

(About half a page: which assistants or tools you used and for what. If you used none, say so.)

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

### 1d. Decision (at most 150 words)

Chosen candidate: B, k=5
I choodsed B, k=5 because its annual cost is $12,912.73, within the $15,000 budget. It has higher recall than B, k=3, and their 95% Wilson intervals do not overlap. Recall@5 is 70% for EN (14/20), 75% for RU (15/20), and 70% for KK (14/20). EN and KK have the lowest recall for this choice. Configurations A exceed the annual budget.
(Decision, using your intervals and the budget. Give the recall of your choice for EN, RU and KK separately.)

### 1e. Next measurement (at most 60 words)
Evaluate A, k=3 and B, k=5 on a larger independently labelled test set, with at least 100 questions per language. Compare per-language recall and 95% Wilson intervals to check whether the observed differences persist and whether the budget-feasible choice remains adequate.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H |0.8833|KK, degraded|0.7333|0.5555|0.8582|14907.51|
| L |0.8056|KK, degraded|0.6333|0.4551|0.7813|18000|

Personal-data pages per year sent abroad under H: 1023825

### 2b. Memo (at most 300 words)
I recommend Pipeline L, subject to a local security and performance acceptance test. H has higher overall accuracy (88.3% versus 80.6%) and lower annual cost ($14,907.51 versus $18,000). However, both pipelines perform worst on degraded Kazakh invoices. H gets 22/30 correct (73.3%; 95% Wilson interval 55.6–85.8%), while L gets 19/30 (63.3%; interval 45.5–78.1%). These intervals are wide, and overall averages hide poorer performance on degraded Kazakh documents.

Under H, approximately 1,023,825 pages containing a name and ИИН would leave Kazakhstan annually. Kazakhstan's personal-data law covers ИИН. Before using H, we must establish where processing occurs, who stores scans and extracted JSON, and how long both are retained. A vendor's statement alone is not a compliance review. For L, processing stays on the bank's server, but we must still verify administrator access, logs, backups, and deletion practices.

Safeguards should include role-based access, encryption in transit and at rest, restricted logging of personal data, tested deletion and retention rules, and a documented audit of data flows. We should measure accuracy by language and scan condition before deployment. L reduces cross-border exposure but costs $3,092.49 more per year and has lower measured accuracy. Its residual risk is extraction error, especially on degraded Kazakh documents; uncertain fields should be sent for human review.

## Part 3: Explain your own numbers

### Q1

Number: 2.73
Why (at most 40 words): The bill ratio differs from the total-token ratio because input and output tokens have different prices. Output tokens cost six times as much as input tokens, and the two languages have different input/output mixes.


### Q2

Number: 355
Why (at most 40 words): Scaling gives 576 × 263/256 ≈ 592 e5 tokens; 60% is about 355. The sentence starts before the 512-token limit and is short enough to fit, so it can be included. Truncation beyond the limit may be silent.

### Q3

Number: 45.5%
Why (at most 40 words): Increasing temperature softens the probability distribution without changing the ranking of these tokens. All five tokens still have nonzero sampling probability; temperature changes their relative probabilities, not the candidate set.

### Q4

Number: 30.4%
Why (at most 40 words): I excluded arithmetic sequences and multiplication because their answers can be derived algorithmically. The birthday and synthetic account-number sets contain one-off facts. A system prompt cannot supply missing factual knowledge or guarantee correct recall.

### Q5

Number: 4.25
Why (at most 40 words): The model has about 85 tokens per parameter, compared with Chinchilla's 20. By this criterion it is over-trained in tokens relative to its parameter count. Chinchilla argued that models such as GPT-3 were under-trained and could use more training tokens for their size.
