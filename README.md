# AI-Powered Customer Support Intelligence System

This project demonstrates the design and implementation of AI-powered workflows for customer support systems, including email classification, sentiment analysis, and knowledge-base question answering. The goal was to build simple, modular, and interpretable solutions using a combination of rule-based logic, prompt engineering, and retrieval-augmented generation (RAG).

---

## Part A — Email Tagging Mini-System

**Problem:**
We have a small dataset of customer support emails. Each email has a subject, body, customer ID, and a ground truth tag. The main challenge is that **tags are customer-specific**, so tags from one customer must not influence another.

**Approach:**

* Built a **baseline text classifier** using a combination of rule-based patterns and a simulated LLM.
* Ensured **customer isolation** by filtering only tags relevant to the current customer during prediction.
* Added **guardrails** to catch words or patterns that commonly mislead the classifier (anti-patterns).
* Used a simple fallback strategy to always assign at least one plausible tag.

**Error Analysis:**

* Most errors occurred when emails were short or ambiguous.
* Misclassifications helped me identify anti-patterns and update rules.

**Ideas for Production:**

1. Replace the simulated LLM with an actual LLM API for better semantic understanding.
2. Expand rules with regex and keyword lists to improve accuracy.
3. Maintain a dynamic feedback loop to retrain rules from new emails.

---

## Part B — Sentiment Analysis Prompt Evaluation

**Problem:**
Hiver uses sentiment for Analytics and Automations. I had to test whether a prompt to an LLM produces **consistent sentiment predictions with reasoning**.

**Approach:**

* Drafted **Prompt v1** to classify sentiment as positive/neutral/negative with confidence and hidden reasoning.
* Tested it on 10 sample emails.
* Observed where the model failed (mostly neutral emails being misclassified).
* Created **Prompt v2** to improve consistency and confidence scoring.

**Findings:**

* Prompt v2 improved consistency and gave clearer reasoning behind predictions.
* Confidence scores helped identify low-certainty predictions for debugging.

**How to Evaluate Prompts Systematically:**

1. Prepare a labeled test set.
2. Compare outputs with ground truth.
3. Identify failure patterns and iterate prompts accordingly.

---

## Part C — Mini-RAG for Knowledge Base Answering

**Problem:**
Hiver Copilot answers queries using knowledge base (KB) articles. I built a simple **retrieval-augmented generation (RAG)** system.

**Approach:**

* Converted 5–10 KB articles into embeddings using **sentence-transformers**.
* Retrieved top relevant articles based on cosine similarity for a given query.
* Generated answers with a confidence score.

**Example Queries:**

1. “How do I configure automations in Hiver?”
2. “Why is CSAT not appearing?”

**Results:**

* System retrieved relevant articles and generated answers for both queries.
* Confidence scores reflected retrieval quality.

**Ideas to Improve Retrieval:**

1. Use larger or OpenAI embeddings for better semantic understanding.
2. Implement caching for repeated queries.
3. Expand the KB for broader coverage.
4. Add query reformulation for harder queries.
5. Include confidence scoring for answer reliability.

**Failure Case & Debugging:**

* Rare mismatches occurred with short, ambiguous queries.
* Debugged by checking similarity scores and top-K retrieved articles.

---

## How to Run

1. Clone the repository.
2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Run the notebooks in order:

   * `Part_A.ipynb`
   * `Part_B.ipynb`
   * `Part_C.ipynb`

All notebooks are **self-contained** and can be run end-to-end.

---

## Key Highlights
- Built a modular email tagging system with customer-level isolation
- Designed and evaluated multiple LLM prompts for sentiment consistency
- Implemented a mini RAG pipeline for knowledge base retrieval
- Performed error analysis and iterative improvements

---

Note: This project was inspired by a real-world evaluation scenario and extended with additional improvements and analysis.
