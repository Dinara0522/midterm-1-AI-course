# Midterm 1: your data

GitHub username: `dinara0522` · session code: `maple-66` · generator v1

**Fingerprint: `3841b484`**: copy it into the first lines of `ANSWERS.md`. All numbers below are synthetic: this is an exam, not a measurement.

## Part 1: inputs

`retrieval_ranks.csv`: 60 test questions (20 EN, 20 RU, 20 KK). `rank_A` and `rank_B` give the position of the correct chunk in the top 10 retrieved under config A and config B; **11 means the correct chunk was not in the top 10.**

Production traffic and Model M token counts (tokens per item, as counted by Model M's tokenizer):

| language | share of traffic | question tokens | answer tokens | chunk A tokens | chunk B tokens |
|---|---|---|---|---|---|
| EN | 28 % | 28 | 120 | 257 | 73 |
| RU | 37 % | 55 | 235 | 504 | 143 |
| KK | 35 % | 73 | 312 | 668 | 190 |

- Requests per day: **7,500**, in the traffic shares above.
- System prompt: **227** tokens in every request.
- Price: **$2** per million input tokens, **$12** per million output tokens.
- Annual budget for this service (model calls only): **$15,000**.

## Part 2: inputs

`doc_results.csv`: for each pipeline, language and scan condition, `n_docs` test invoices and `n_correct` = invoices whose number, date, seller ID and total were all extracted exactly (strict scorer, as in Lab 04).

- **Pipeline H**: hosted vision-language API in a data centre abroad, pay per token; each page is sent as an image.
- **Pipeline L**: open vision-language model on your own server in Kazakhstan, fixed monthly cost.

- Volume: **8,500** scanned pages per day. In **33 %** of them an individual's name and ИИН are printed (sole proprietors, receipts).
- Page image: **1240 × 1754** pixels. Pipeline H counts an image as ⌈width ÷ 28⌉ × ⌈height ÷ 28⌉ input tokens and returns about **394** output tokens per page (the JSON).
- Pipeline H price: **$1** per million input tokens, **$5** per million output tokens.
- Pipeline L: one server costs **$750** per month and handles up to **6,000** pages per day; add servers as needed.

## Part 3: your five questions

Answer each in `ANSWERS.md`: one **Number** line and one **Why** line of at most 40 words.

### Q1

The same support request, once in English and once in Kazakh, through Model M ($2 per million input tokens, $12 per million output tokens):

| | input tokens | output tokens |
|---|---|---|
| EN | 1,510 | 114 |
| KK | 4,669 | 219 |

Compute the token ratio (total tokens KK ÷ EN) and the bill ratio (cost KK ÷ cost EN). **Number:** the bill ratio (2 decimals). **Why** (at most 40 words): why is the bill ratio not equal to the token ratio?

### Q2

A teammate sets the chunk size to **576 tokens, counted with cl100k**. The retrieval model (e5-small) reads at most 512 of *its own* tokens. Assume e5 tokens grow in proportion to cl100k tokens at the rate measured in Lecture 4.1 (a chunker told 256 cl100k tokens produced chunks of 263 / 128 / 76 e5 tokens for EN / RU / KK), and that every chunk is exactly the full size.

In an English chunk, the sentence that contains the answer starts 60 % of the way into the chunk and is shorter than 20 e5 tokens. **Number:** the position of the start of that sentence, in e5 tokens (nearest integer). **Why** (at most 40 words): can a question that matches only that sentence retrieve this chunk, and would you see an error?

### Q3

A language model gives these next-token scores for the prompt "The branch is closed on":

| token | score |
|---|---|
| Monday | 4.7 |
| Friday | 3.9 |
| Sunday | 2.8 |
| holiday | 2.5 |
| Easter | 1.2 |

Apply softmax at temperature T = 1.5. **Number:** the probability of the top token, in percent (1 decimal). **Why** (at most 40 words): what did changing T do to the ranking of the tokens, and to the set of tokens that can be sampled?

### Q4

A base model (pre-training only) is evaluated on four question sets. For each set, the table gives how many questions it has and the share of its facts that appear exactly once in the training corpus:

| set | questions | facts seen exactly once |
|---|---|---|
| Continuing arithmetic sequences | 187 | 1 % |
| Two-digit multiplication | 142 | 3 % |
| Birthdays of public figures | 231 | 33 % |
| Account numbers in synthetic bank profiles | 180 | 27 % |

**Number:** the lower bound on the expected share of wrong answers, in percent (1 decimal), over all questions in the sets where such a bound applies. **Why** (at most 40 words): which sets did you leave out and why, and would a system-prompt instruction "never invent a fact" change the bound?

### Q5

A lab trains a model with **13 billion parameters on 1.105 trillion tokens**. Chinchilla (Lecture 1.1) trained 70 billion parameters on 1.4 trillion tokens, which the paper presents as the compute-optimal ratio. **Number:** this model's tokens per parameter divided by Chinchilla's tokens per parameter (2 decimals). **Why** (at most 40 words): is the model under- or over-trained by that criterion, and what did Chinchilla say about models such as GPT-3?
