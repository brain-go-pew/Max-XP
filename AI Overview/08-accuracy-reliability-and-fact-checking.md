# 08 Accuracy, Reliability & Fact-Checking

AI answers sound equally confident whether they are right or wrong, and people increasingly act on them without checking.

---

## 8.1 Why Accuracy Matters: Real Failures

### Google AI Overviews (May 2024)

Within days of launch, it told people to add **"non-toxic glue" to pizza sauce** (from an 11-year-old joke Reddit comment) and said **geologists recommend eating a small rock a day** (from satire site The Onion). It retrieved real pages but couldn't tell jokes from facts. Google then restricted AI Overviews on nonsensical queries and relied less on forum content.

### Fake legal citations

In **Mata v. Avianca** (2023) a New York lawyer cited cases ChatGPT invented and was sanctioned. Damien Charlotin's database listed **1,624 court cases** with AI-fabricated content as of 18 June 2026. Courts now fine lawyers thousands of dollars.

### Why it matters

One confident error can mislead millions at once, damage a brand and create legal liability.

### Expanded context from Research Notes

**Example 1: Google AI Overviews (May 2024).** Within days of launch to all US users, AI Overviews told people to add "non-toxic glue" to pizza sauce so cheese would stick, an idea traced to an 11-year-old joke Reddit comment, and said geologists recommend eating a small rock a day, lifted from a satirical article by The Onion. The system retrieved real pages but could not tell jokes and satire from facts. Google responded by restricting AI Overviews on nonsensical queries and relying less on user-generated forum content.

**Example 2: Fake legal citations.** In 2023, a New York lawyer filed a brief citing court cases invented by ChatGPT (Mata v. Avianca), and the judge sanctioned him. It has since become widespread: researcher Damien Charlotin's public database listed 1,624 court cases involving AI-fabricated content as of 18 June 2026, most from the US. Courts now fine lawyers thousands of dollars for unchecked AI citations.

**Why it matters.** AI is used for health, legal, financial and news questions. A single confident error can mislead millions of users at once, damage trust in a brand, and create legal liability.

---

## 8.2 Hallucinations

A **hallucination** is a fluent, plausible statement that is false or unsupported. The model isn't "seeing" things; it is generating likely-sounding text.

### Types of hallucination

| Type | What happens | Example |
|------|--------------|---------|
| **Factual (from memory)** | Invents a fact | Wrong birthday, made-up statistic |
| **Fabricated source** | Invents a reference, quote or URL | A fake court case or paper |
| **Unfaithful (grounded)** | Has the right source but misstates or adds to it | Summary says "40%," article says "14%" |
| **Misattribution** | Correct claim, wrong source | Quote credited to the wrong newspaper |

### Why they happen (OpenAI, "Why Language Models Hallucinate," 2025)

1. **Pretraining:** next-word prediction learns regular patterns, but rare, arbitrary facts can't be predicted, so the model guesses.
2. **Evaluation rewards guessing:** benchmarks score only accuracy. Like a test with no penalty for wrong answers, guessing beats "I don't know."

### The paper's example

A model that abstained 52% of the time had a **26% error rate**; an older model that almost always answered had slightly higher accuracy but a **75% error rate**.

**Fix:** penalize confident errors more than honest uncertainty.

### How often?

Summarizing a supplied document: models added unsupported content to **1.8%–24.2%** of summaries (Vectara, May 2026, 100+ models). From memory, rates are far higher, and benchmarks often rank models differently.

### Expanded context from Research Notes

A hallucination is a fluent, plausible-sounding statement from an AI that is false or not supported by any source. The term is borrowed loosely from psychology; the model isn't "seeing" things, it is generating likely-sounding text.

**Main types** (same table as above):

| Type | What happens | Example |
|------|--------------|---------|
| **Factual (from memory)** | Invents a fact the model doesn't actually know | Wrong birthday, made-up statistic |
| **Fabricated source** | Invents a reference, quote or URL | A fake court case or research paper |
| **Unfaithful (grounded)** | Has the right source but misstates or adds to it | Summary says "40%" when the article says "14%" |
| **Misattribution** | Correct claim, wrong source | Quote credited to the wrong newspaper |

**Why they happen.** OpenAI's 2025 paper "Why Language Models Hallucinate" gives two reasons:

1. **Pretraining:** models learn by predicting the next word from huge amounts of text that has no "true/false" labels. Regular patterns like spelling are learned reliably, but rare, arbitrary facts (like someone's birthday) can't be predicted from patterns, so the model guesses something plausible.
2. **Evaluation rewards guessing:** most benchmarks score only accuracy. Like a student on a multiple-choice test with no penalty for wrong answers, a model that guesses scores higher than one that says "I don't know." So training pushes models toward confident guessing.

**The paper's example:** on one test, a model that abstained 52% of the time had a 26% error rate, while an older model that almost always answered had slightly higher accuracy but a 75% error rate. The suggested fix is to penalize confident errors more than honest uncertainty.

**How often?** It depends heavily on the task:
- **Summarizing a supplied document:** on Vectara's leaderboard (May 2026, 100+ models), models added unsupported content to between 1.8% and 24.2% of summaries.
- **Answering from memory, with no source:** rates are far higher, and different benchmarks often rank the same models very differently.
- **Web search** helps but doesn't eliminate errors (see the Tow Center citation study in the AI Search notes).

---

## 8.3 Techniques That Improve Accuracy

No single fix exists, so reliable systems **stack layers**; if one misses an error, the next can catch it.

### The accuracy stack

| Technique | How it works | What it fixes |
|-----------|--------------|---------------|
| **Grounding with RAG** | Answer only from trusted retrieved documents | The model "never had the fact" |
| **Citations** | Every claim points to a passage | Makes errors traceable |
| **Claim-level verification** | Split into claims, check each, drop unsupported ones | Citations that don't support the claim |
| **Chain-of-Verification (CoVe)** | Draft → generate check questions → answer them independently → revise | Self-contradictions, invented details |
| **Self-consistency** | Generate several answers; trust what most agree on | Random one-off guesses |
| **Abstention** | Allow and reward "I don't know" | Confident guessing |
| **Second-model review** | A separate model checks for unsupported claims | Errors a model can't see in itself |
| **Human review** | Spot-check samples and high-stakes answers | Everything automation misses |

### Limits

Citations alone don't guarantee accuracy, and each check adds time and cost, so products trade speed against reliability.

Grounding turns the model from "source of truth" into "reader and summarizer of trusted sources."

### Example

A company help bot: answer only from the policy documents, cite the section for every claim, and if the documents don't cover it, say so and offer a human agent.

### Expanded context from Research Notes

No single fix removes hallucinations, so reliable systems stack several layers. If one layer misses an error, the next can catch it.

| Technique | How it works | What it fixes |
|-----------|--------------|---------------|
| **Grounding with RAG** | Retrieve trusted documents and tell the model to answer only from them | The model "never had the fact" |
| **Citations** | Every claim must point to a specific retrieved passage | Makes errors traceable and checkable |
| **Claim-level verification** | Split the answer into individual claims and check each against the sources; drop or flag unsupported ones | Citations that don't actually support the claim |
| **Chain-of-Verification (CoVe)** | Draft an answer, generate check questions, answer them independently, then revise | Self-contradictions and invented details |
| **Self-consistency** | Generate several answers; trust only what most of them agree on | Random one-off guesses |
| **Abstention** | Allow and reward "I don't know" or "not enough information" | Confident guessing |
| **Second-model review (guardrails)** | A separate model checks the output for unsupported claims | Errors the first model can't see in itself |
| **Human review** | People spot-check samples and high-stakes answers | Everything automated checks miss |

**Important limits.** Citations alone don't guarantee accuracy: a model can cite the wrong passage or add claims the passage doesn't contain. Every extra verification step also adds time and cost, so products balance speed against reliability.

**Why it matters.** Grounding turns the model from "source of truth" into "reader and summarizer of trusted sources," which is why AI search tools retrieve before they answer.

**Example.** A company help bot is told: answer only from the policy documents provided, cite the section for every claim, and if the documents don't cover the question, say so and offer a human agent.

---

## 8.4 Source Conflicts

Researchers call disagreements **knowledge conflicts**: context vs memory (a fresh source differs from training data), between sources, and within memory.

### DRAGged into Conflicts (Google Research, 2025)

The right behavior depends on **why** sources disagree:

| Conflict type | Example | Best behavior |
|---------------|---------|---------------|
| **Complementary details** | Sources add different details about one event | Combine them |
| **Outdated information** | Older vs newer counts of ISS visitors | Prefer the most recent reliable source; mention the date |
| **Differing opinions / research** | Is fasting good for people with diabetes? | Present main views fairly; don't pick a side as fact |
| **Misinformation / satire** | Satire site vs geologists on eating rocks | Rely on credible sources; ignore or flag the bad one |

### Findings

Their CONFLICTS benchmark found LLMs often handle conflicts poorly, but prompting the model to first reason about **what kind of conflict it is** significantly improved answers. Models also sometimes stick to outdated memory over a newer document.

### Example

"Is coffee good for you?" should note benefits, risks and that it depends on amount and person.

### Expanded context from Research Notes

Retrieved sources often disagree with each other, or with what the model "remembers" from training. Researchers call these **knowledge conflicts**, in three kinds:

- **Context vs. memory:** a fresh source says something different from the model's training data (e.g., a new world record).
- **Between sources:** two retrieved pages contradict each other.
- **Within memory:** the model's own stored knowledge is inconsistent.

A 2025 Google Research study ("DRAGged into Conflicts") argues there's no single rule; the right behavior depends on why sources disagree:

| Type of conflict | Example | Best behavior |
|------------------|---------|---------------|
| **No real conflict / complementary details** | Sources add different details about the same event | Combine them |
| **Outdated information** | Older and newer counts of people who have visited the ISS | Prefer the most recent reliable source, mention the date |
| **Differing opinions or research results** | Is fasting good for people with diabetes? | Present the main views fairly; don't pick a side as fact |
| **Misinformation or satire** | A satire site vs. real geologists on eating rocks | Rely on credible sources and ignore or flag the bad one |

**Other findings:** models sometimes stick to outdated training memory instead of a newer document, and mixing conflicting facts with irrelevant noise can sharply reduce answer quality.

**Why it matters.** AI search often blends many sources into one confident paragraph, which can hide real disagreement. A good answer says when experts disagree or when information has changed.

**Example.** Asked "Is coffee good for you?", a careful answer notes benefits found in some studies, risks in others, and that results depend on amount and person, rather than a single yes or no.

---

## 8.5 Evaluating Answer Quality

### 1. Benchmarks with known answers

SimpleQA, Vectara's leaderboard, the Tow Center test. They often disagree, and accuracy-only scoring rewards guessing.

### 2. RAGAS (Es et al., 2023): four scores from 0 to 1

| Metric | Question | Tests |
|--------|----------|-------|
| **Faithfulness** | Is every claim supported by the retrieved sources? | Generator |
| **Answer relevance** | Does the answer address the question? | Generator |
| **Context precision** | Were the retrieved passages relevant? | Retriever |
| **Context recall** | Did retrieval find everything needed? | Retriever |

**Faithfulness** = supported claims ÷ total claims (3 of 5 → 0.6).

A confidently wrong answer can still score high on relevance, so metrics are used together.

### 3. Judges

- **Human evaluation:** most trustworthy, slow, expensive.
- **LLM-as-a-judge:** fast, scalable, but may share blind spots, so check against humans.

### Expanded context from Research Notes

Measuring how good AI answers are, so developers can compare models and catch problems. There are three main approaches.

**1. Benchmarks with known answers.** Test sets of questions with correct answers, scored automatically. Examples: SimpleQA (short factual questions), Vectara's leaderboard (faithfulness of summaries), the Tow Center citation test. Limitation: benchmarks often disagree with each other, and accuracy-only scoring rewards guessing (see section 8.2).

**2. RAG quality metrics (RAGAS).** RAGAS, introduced by Es et al. in 2023, is a popular open-source framework that scores AI search and RAG systems from 0 to 1 on four metrics:

| Metric | Question it answers | Tests which part |
|--------|---------------------|------------------|
| **Faithfulness** | Is every claim in the answer supported by the retrieved sources? | Generator |
| **Answer relevance** | Does the answer actually address the question? | Generator |
| **Context precision** | Were the retrieved passages relevant? | Retriever |
| **Context recall** | Did retrieval find everything needed? | Retriever |

**How faithfulness is measured:** break the answer into simple claims, check each against the sources, and divide supported claims by total claims. If 3 of 5 claims are supported, faithfulness = 0.6.

**Watch out:** a confidently wrong answer can still score high on relevance, which is why metrics are used together.

**3. Human and AI judges.** Human evaluation: experts or trained raters judge correctness, completeness and helpfulness. Most trustworthy, but slow and expensive. LLM-as-a-judge: another AI model scores answers using a rubric. Fast and scalable, but the judge can share the same blind spots, so it must be checked against human ratings.

**Why it matters.** "Accuracy" isn't one number. A good evaluation asks: Is it true? Is it supported by the cited sources? Does it answer the question? Did it admit uncertainty when it should?

---

## 8.6 Fact-Checking AI Answers Yourself: SIFT

Developed by digital-literacy expert **Mike Caulfield**.

| Step | Ask yourself |
|------|--------------|
| **S — Stop** | Do I know where this came from? Is it surprising or too perfect? |
| **I — Investigate the source** | Open the cited link. Expert, official body, forum post, or satire? |
| **F — Find better coverage** | Do other trusted sources say the same? |
| **T — Trace claims to the original** | Find the original study, quote or data. Did the AI change numbers, dates or meaning? |

### Lateral reading

The core skill: open new tabs to see what other sources say about a page, instead of reading one page very closely. Stanford found professional fact-checkers judge sources more accurately this way.

### Checklist

- Each important claim cited?
- Does the page actually say that?
- Is it recent enough?
- Do two independent credible sources agree?
- Does the answer mention uncertainty?

### Example

An AI says a new law took effect last month and cites a news site. Clicking through shows the law was only **proposed**. The answer had a citation and was still wrong.

### Expanded context from Research Notes

The SIFT method, developed by digital literacy expert Mike Caulfield, is a quick routine professional fact-checkers use. It works just as well on AI answers.

1. **S — Stop.** Before you trust or share an answer, pause. Do you know where this came from? Is it surprising or too perfect?
2. **I — Investigate the source.** Open the cited link. Who wrote it? Is it a real expert, an official body, a forum post, or satire?
3. **F — Find better coverage.** Search for the claim elsewhere. Do other trusted sources say the same thing?
4. **T — Trace claims to the original.** Find the original study, quote or data. Check the AI didn't change numbers, dates or meaning.

**Lateral reading** is the core skill: instead of reading one page very carefully, open new tabs and see what other sources say about that page and claim. Stanford researchers found professional fact-checkers judge sources more accurately this way.

**Quick checklist for AI answers:**
- Does each important claim have a citation?
- Does the cited page actually say that?
- Is the source recent enough for the question?
- Do at least two independent, credible sources agree?
- Does the answer mention disagreement or uncertainty where it exists?

**Why it matters.** AI tools rarely flag their own uncertainty. Users are the last line of defense, especially for health, legal, financial and news topics.

**Example.** An AI says a new law took effect last month and cites a news site. Clicking through shows the article says the law was only proposed, so the answer was wrong even though it had a citation.

---

## Try it yourself

### Activity 8.1 · Spot the errors

This AI-style answer has three mistakes. Find and fix them:

> "The Tow Center found AI search tools were wrong about 16% of the time. Perplexity was the least accurate. SIFT stands for Search, Investigate, Find, Trust."

**Answers:**
- Wrong **60%+** of the time (not 16%)
- Perplexity was the **most** accurate (Grok 3 worst)
- SIFT = **Stop, Investigate the source, Find better coverage, Trace claims to the original**

---

### Activity 8.2 · SIFT a real answer (try with a chatbot)

Ask a chatbot a health or science question. Pick one claim from its answer and run all four SIFT steps. Also count: of the claims in the answer, how many could you confirm? Divide to get your own faithfulness score.

**What to notice / answers:** E.g. 6 of 8 claims supported = **0.75**.

---

## KEY TAKEAWAYS

- Hallucinations come from pretraining and from evaluation that rewards guessing.
- Reliable systems stack layers: grounding, citations, verification, abstention, review.
- Handle conflicts by type; measure quality with RAGAS, benchmarks and judges.
- You are the last line of defense: use SIFT.

---

## Key terms

| Term | Definition |
|------|------------|
| **Faithfulness** | Whether an answer sticks to what its sources say. |
| **Factuality** | Whether an answer is true in the real world. |
| **Abstention** | The model choosing to say "I don't know." |
| **Calibration** | How well a model's confidence matches its accuracy. |
| **Knowledge conflict** | Sources (or source vs memory) disagreeing. |
| **LLM-as-a-judge** | Using an AI to grade another AI's answers. |
| **Lateral reading** | Checking a source by seeing what others say about it. |

### Additional key terms (from Research Notes)

| Term | Definition |
|------|------------|
| **Hallucination** | A fluent but false or unsupported statement from an AI. |
| **Grounding** | Basing an answer on supplied, trusted sources. |
| **Chain-of-Verification** | Draft, check with questions, then revise. |
| **RAGAS** | Framework scoring faithfulness, relevance, context precision and recall. |
| **SIFT** | Stop, Investigate, Find better coverage, Trace claims. |

---

## Sources (from Research Notes)

1. The Journal.ie, Why Google told people to eat rocks and glue cheese to pizza
2. The Register, Google addresses bizarre AI search results
3. Vibe Graveyard, Google's AI Overviews says to eat rocks
4. Vaquill, Charlotin AI hallucination tracker (1,624 cases)
5. Bloomberg Law, AI faked cases irritate judges
6. OpenAI, Why language models hallucinate
7. Kalai et al., Why Language Models Hallucinate (arXiv)
8. Vectara Hallucination Leaderboard (GitHub, via LongtermWiki)
9. Uvik, AI hallucination rates
10. TestMu AI, What each hallucination benchmark measures
11. KDnuggets, 7 Ways to Reduce Hallucinations in Production LLMs
12. Machine Learning Mastery, 7 prompt engineering tricks to mitigate hallucinations
13. Machine Learning Mastery, 5 techniques beyond prompt engineering
14. CustomGPT, Reduce AI hallucinations (citations vs. verification)
15. MemX, How to reduce LLM hallucinations
16. Cattan et al., DRAGged into Conflicts (arXiv)
17. Google Research, (D)RAGged into a Conflict
18. What Is Seen Cannot Be Unseen: knowledge conflict in LLMs (arXiv)
19. AITopics, Conflicting knowledge research
20. Let's Data Science, RAGAS and LLM-as-Judge
21. Manning, RAG evaluation chapter
22. University of Washington CIP, Find Trustworthy Information (SIFT)
23. Wellesley College Library, Using SIFT to verify information
24. UC Merced Library, The SIFT Method
25. Simon Willison, The SIFT method
