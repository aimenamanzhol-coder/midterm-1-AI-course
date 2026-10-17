# Midterm 1: answers

GitHub username: aimenamanzhol-coder
Session code: ZEBRA-28
Fingerprint: 1c23dab5

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration
I used ChatGPT and Google Colab while completing this midterm.

I used Google Colab to run the provided Python notebook and generate my individual dataset using my GitHub username and the session code.

I used ChatGPT to help calculate retrieval metrics, Wilson confidence intervals, annual costs, document-processing accuracy, and the numerical answers in Part 3. ChatGPT also helped me compare the available configurations and pipelines, draft explanations and recommendations in English, and format the answers in GitHub.

I reviewed the generated results and used the course formulas and assignment instructions to understand the calculations. I understand that I am responsible for the submitted answers and must be able to explain them during the oral check.

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)


| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A | 0.4667 | 0.7167 | 0.7667 | 0.5975 |
| B | 0.1833 | 0.4167 | 0.6667 | 0.3511 |
### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.7167 | 0.5923 | 0.8149 |
| A, k=5 | 0.7667 | 0.6456 | 0.8556 |
| B, k=3 | 0.4167 | 0.3006 | 0.5427 |
| B, k=5 | 0.6667 | 0.5406 | 0.7727 |

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 34219.24 |
| A, k=5 | 45984.00 |
| B, k=3 | 21294.90 |
| B, k=5 | 24443.43 |

### 1d. Decision (at most 150 words)

Chosen candidate: A, k=3

I choose configuration A with k=3 because it provides the highest observed recall among the options within the annual budget of $40,100.

Its overall recall is 71.67%, and its annual cost is $34,219.24. The recall is 70% for English, 80% for Russian, and 65% for Kazakh. This means Kazakh-speaking users receive the weakest retrieval performance.

Configuration A with k=5 achieves higher recall, but its cost exceeds the budget. Configuration B with k=5 is cheaper, but its observed recall is lower. However, their Wilson confidence intervals overlap, so the evidence does not establish a clear statistical difference between A with k=3 and B with k=5.

I recommend A with k=3 while continuing to monitor performance across all three languages.


### 1e. Next measurement (at most 60 words)
I would test A with k=3 and B with k=5 on 300 additional questions, using 100 questions for each language (EN, RU, KK). I would compare recall and Wilson intervals to check whether the observed difference is reliable, especially for Kazakh, which currently has the lowest recall.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | 0.8833 | KK, degraded | 0.8000 | 0.6269 | 0.9050 | 10344.10 |
| L | 0.8222 | KK, degraded | 0.6333 | 0.4551 | 0.7813 | 5400 |

Personal-data pages per year sent abroad under H: 569400

### 2b. Memo (at most 300 words)
To: Head of Operations

Subject: Recommendation for Invoice Processing Pipeline

I recommend Pipeline L, with additional quality controls, because it processes documents locally in Kazakhstan and costs $5,400 per year, compared with $10,344.10 for Pipeline H.

Pipeline H has higher overall accuracy (88.33%) than Pipeline L (82.22%). However, both perform worst on degraded Kazakh-language scans. H achieves 80.00% accuracy (95% Wilson interval: 62.69%–90.50%), while L achieves 63.33% (45.51%–78.13%). These intervals overlap, so the sample does not establish a clear difference for this group. Overall accuracy also hides the weaker results for these users.

Under H, 569,400 pages containing personal data would be sent abroad annually. We must verify where the images are processed, who stores them, and how long they are retained. We also need to investigate vendor access, subcontractors, deletion policies, and compliance with Kazakhstan's personal-data requirements.

With L, processing remains on the bank's local server, but internal storage, access permissions, and retention periods must still be controlled.

I recommend encryption, restricted access, audit logs, verified deletion procedures, and human review of low-confidence results. These measures should be tested regularly.

The main remaining risk is Pipeline L's lower accuracy on degraded Kazakh documents. Additional testing, better scan quality, and human verification are necessary before full deployment.

## Part 3: Explain your own numbers

### Q1

Number: 2.11

Why (at most 40 words): The bill ratio differs from the token ratio because input and output tokens have different prices. Output tokens cost five times more, and the English and Kazakh requests have different proportions of input and output tokens.

### Q2
Number: 13.5%

Why (at most 40 words): Only English chunks exceed the 512-token e5 limit. Their final 13.5% is truncated and invisible to the embedding model, so information in that portion cannot influence retrieval. Russian and Kazakh chunks remain within the limit.


### Q3
Number: 94.1%

Why (at most 40 words): Lowering the temperature to 0.4 makes the probability distribution sharper and favors the highest-scoring token. The ranking of tokens does not change. All five tokens still have nonzero probabilities and can be sampled.


### Q4
Number: 34.0%

Why (at most 40 words): I excluded multiplication and arithmetic sequences because they test rule-based reasoning rather than recall of individual facts. The remaining sets contain rare facts. A system prompt cannot make the model reliably know facts that it did not learn during training.

### Q5
Number: 39312

Why (at most 40 words): The first message is billed 27 times because the full conversation history is resent on every turn. Prompt caching can reduce the cost of repeated tokens, but it does not remove them from the conversation context.

