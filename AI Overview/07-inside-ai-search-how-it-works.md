# 07 Inside AI Search: How It Works

An AI search engine is not one model. It is a pipeline: a search system finds evidence, and a language model writes an answer from that evidence.

---

## 7.1 The Pipeline: From Query to Cited Answer

| Step | What happens |
|------|--------------|
| **1. Query understanding** | An LLM works out what you want (fact, comparison, how-to, shopping, local) and rewrites the question into better search terms. Simple questions ("capital of Spain") skip most heavy steps. |
| **2. Query fan-out** | Complex questions split into many sub-questions searched at once. Google: AI Mode "breaks down your question into subtopics and issues a multitude of queries simultaneously." A second round can fill gaps. |
| **3. Retrieval** | Each sub-query searches a huge index (Google's own, Perplexity's own, or Bing for some tools), combining keyword search (exact words) with semantic search (meaning). |
| **4. Ranking and reranking** | Hundreds of candidates are scored for relevance, freshness and trust; a more careful reranker picks the best few. |
| **5. Chunking and context** | The most useful passages (not whole pages) go into the LLM's prompt with their URLs, each tagged with a number. |
| **6. Generation** | The LLM writes mainly from the supplied passages: retrieval-augmented generation (RAG). |
| **7. Citation attribution** | Claims are linked to the passage numbers they came from (footnotes, chips or links). |
| **8. Checks and display** | Safety and quality checks; formatting with links, images, tables, follow-up suggestions. A follow-up repeats the process with the conversation as context. |

### Expanded context from Research Notes

The Research Notes describe the same pipeline in detail:

**1. Query understanding.** An LLM works out what you actually want (a fact, a comparison, a how-to, shopping, local results) and rewrites the question into better search terms. Simple questions like "capital of Spain" skip most of the heavy steps.

**2. Query fan-out.** For complex questions the system splits one question into many sub-questions and searches them all at once. Google says AI Mode "breaks down your question into subtopics and issues a multitude of queries simultaneously." If gaps remain, it can run a second round.

**3. Retrieval.** Each sub-query searches a huge index of web pages (Google's own index, Perplexity's own index, or Bing for some tools). Modern systems combine keyword search (exact words) with semantic search (matching meaning).

**4. Ranking and reranking.** Hundreds of candidate pages are scored for relevance, freshness and trustworthiness. A second, more careful model (a reranker) then picks the best few.

**5. Chunking and context building.** The system pulls out the most useful passages (not whole pages) and places them, with their source URLs, into the LLM's prompt. Each passage is tagged with a number so it can be cited later.

**6. Generation (grounded answer).** The LLM writes an answer using mainly the supplied passages, not just its memory. This is called retrieval-augmented generation (RAG).

**7. Citation attribution.** Claims in the answer are linked to the passage numbers they came from, shown as footnotes, chips or links.

**8. Checks and display.** Safety filters and quality checks run; the answer is formatted with links, images, tables or follow-up suggestions. A follow-up question repeats the whole process with the conversation as context.

### Why it matters

Each step can fail on its own (weak search, wrong ranking, a model misreading a correct source). That's why answers can be impressive and wrong.

### Fan-out example

"Is it better to visit Japan in spring or autumn for a first trip?" → searches on cherry-blossom dates, autumn-foliage season, crowds, prices and weather. The answer combines them and cites a travel guide, a weather site and a booking site.

### Expanded context from Research Notes

The Research Notes give the same example: "Is it better to visit Japan in spring or autumn for a first trip?" might fan out into searches on cherry-blossom dates, autumn-foliage season, crowd levels, prices and weather. The answer combines all of them and cites a travel guide, a weather site and a booking site.

---

## What AI Search Is (from Research Notes)

AI search (also called an "answer engine") reads the web for you and writes a direct answer with links to its sources, instead of only showing a list of blue links. Main examples: Google AI Overviews and AI Mode, Perplexity, ChatGPT search, Microsoft Copilot and Gemini.

### Classic search vs AI search

| | Classic search | AI search |
|---|---|---|
| **You get** | A ranked list of links | A written answer + citations |
| **Who does the reading** | You | The AI |
| **Queries run behind the scenes** | Usually one | Often many ("fan-out") |
| **Follow-up questions** | Start a new search | Continue the conversation |
| **Main risk** | Low-quality pages | Confident but wrong answers |

### Why it matters

AI search is now mainstream. Google says AI Overviews reach more than 2 billion monthly users in 200+ countries (some 2026 reports cite 2.5 billion), and AI Mode passed 1 billion monthly users in 2026. It also changes the web's economy: a Pew Research study of 68,879 Google searches found people clicked a regular result in only 8% of visits when an AI summary appeared, vs. 15% without one, and clicked a link inside the summary just 1% of the time.

### Example

Searching "best laptop for video editing under $1,000" in classic search gives ten review sites to compare. AI Mode instead writes a short comparison with recommended models and cites the reviews it used.

---

## 7.2 Key Technology

### RAG (Retrieval-Augmented Generation)

Lewis et al., 2020: retrieve documents first, then generate. A plain LLM only knows its training data (with a cutoff) and may invent facts; RAG adds fresh evidence and makes citations possible.

**Analogy:** closed-book exam → open-book exam.

### Embeddings / vector search

Pages and the query become meaning vectors; the closest are retrieved. "Sunny weather" matches "clear blue skies."

### Hybrid search

Keyword search (BM25) and vector search in parallel, then merged. They fail in opposite ways:
- Keywords catch exact names, codes and rare terms but miss paraphrases.
- Vectors catch paraphrases but miss exact identifiers.

### Reranking

A slower, more accurate model reads the query with each passage. Typical: retrieve ~100, rerank to top 5–10.

Anthropic: contextual embeddings + keyword search + reranking cut retrieval failures by **67%**.

### Grounding

Instructing and training the model to answer only from retrieved sources and cite claims. Reduces hallucination and lets users check.

### Expanded context from Research Notes

**Retrieval-Augmented Generation (RAG)** — What: A method, introduced in research by Lewis et al. (2020), where a model first retrieves relevant documents and then generates an answer from them. Why: An LLM alone only knows its training data (which has a cutoff date) and may invent facts. RAG gives it fresh, specific evidence and makes citations possible. Simple analogy: a closed-book exam (plain LLM) vs. an open-book exam (RAG).

**Embeddings and Vector Search (semantic search)** — What: Text is converted into embeddings, lists of numbers that capture meaning (see the NLP notes). Pages and passages are stored as vectors; the query is also turned into a vector, and the closest vectors are retrieved. Why: It finds matches by meaning: "sunny weather" can match "clear blue skies" even with no shared words.

**Hybrid Search** — What: Running classic keyword search (the BM25 algorithm) and vector search in parallel, then merging the results. Why: They fail in opposite ways. Keyword search is great for exact names, codes and rare terms but misses paraphrases; vector search catches paraphrases but can miss exact identifiers. Together they cover each other's blind spots.

**Reranking** — What: A second, slower but more accurate model reads the query and each candidate passage together and re-scores them. A typical setup retrieves about 100 candidates, then reranks down to the top 5–10 for the LLM. Why: Better evidence in means better answers out. Anthropic reported that combining contextual embeddings, keyword search and reranking cut retrieval failures by 67%.

**Grounding** — What: Instructing and training the model to base its answer only on the retrieved sources and attach citations to specific claims. Why: It reduces hallucination and lets users check the answer.

---

## 7.3 How Citations Are Chosen

A page must survive every stage: be in the index, match a fan-out query, rank highly, and contain a clear quotable passage.

### Helpful signals

- Relevance
- Authority and trust
- Freshness
- Clear structure (headings, lists, direct answers)

### Data

- **Pew:** Wikipedia, YouTube and Reddit = **15%** of links in Google's AI summaries; government sites **6%** (vs 2% in normal results).
- **Perplexity** cites ~5.2 websites per answer vs 3.1 for ChatGPT (23,000+ citations analyzed).

### Mechanism

Each passage gets a number in the prompt; the model adds that number after claims; the interface turns numbers into links.

### Expanded context from Research Notes

**How sources get picked.** A page has to survive every stage of the pipeline: it must be in the index, match one of the fan-out queries, rank highly, and contain a clear passage the model can quote or summarize.

Signals that help include:
- **Relevance:** the passage directly answers a sub-question.
- **Authority and trust:** well-known, expert or official sources with clear authors and evidence.
- **Freshness:** recently updated pages, especially for news, prices and products.
- **Clear structure:** headings, lists and direct answers are easier to extract.

Pew found Wikipedia, YouTube and Reddit made up 15% of links in Google's AI summaries, and government sites 6% (vs. 2% in normal results). An analysis of 23,000+ citations found Perplexity cites about 5.2 different websites per answer, vs. 3.1 for ChatGPT.

**How citation is attached.** Each retrieved passage gets a number in the prompt; the model is told to add that number after each claim it supports. The interface turns the numbers into clickable links.

---

## 7.4 How Accurate Are Citations? (Tow Center, March 2025)

Columbia's Tow Center gave 8 AI search tools 200 real news excerpts and asked them to name the source. **Overall they were wrong more than 60% of the time.**

### Results by tool

| Tool | Result |
|------|--------|
| **Perplexity** | Wrong 37% (best tested) |
| **ChatGPT Search** | Wrong 67%; fully correct only 28% |
| **Grok 3** | Wrong 94% |
| **Gemini and Grok 3** | Over half of responses had made-up or broken URLs |

### Other findings

- Tools rarely admitted uncertainty.
- Paid versions were sometimes worse than free ones.
- Even publishers with licensing deals were often cited wrongly.

### Expanded context from Research Notes

In a March 2025 study, Columbia's Tow Center gave eight AI search tools 200 excerpts from real news articles and asked them to name the source. Overall, they gave incorrect answers more than 60% of the time.

The tools rarely admitted uncertainty, paid versions were sometimes worse than free ones, and even publishers with licensing deals were often cited incorrectly.

**Why it matters:** A citation makes an answer look trustworthy even when the claim doesn't match the source. Always click through for anything important.

---

## 7.5 Comparing Real Tools

| Tool | How it searches | Citation style | Notes |
|------|-----------------|----------------|-------|
| **Google AI Overviews** | Custom Gemini on Google's index; may fan out | Link chips beside summary | Automatic at top of results |
| **Google AI Mode** | Custom Gemini, heavy fan-out | Inline links + side panel | Conversational, multi-turn |
| **Perplexity** | Fresh retrieval every query; own index; hybrid search; multi-stage reranking | Numbered footnotes per claim | Built as an answer engine; best in Tow test |
| **ChatGPT search** | Multiple searches per prompt; architecture not published | Inline source links | Search isn't always triggered |

All follow the same retrieve-then-generate pattern but differ in index, number of searches, and how strictly claims are tied to sources.

### Expanded context from Research Notes

| Tool | Company | How it searches | Citation style | Notes |
|------|---------|-----------------|----------------|-------|
| **AI Overviews** | Google | Custom Gemini on Google's index; may use fan-out | Link chips beside the summary | Appears automatically at the top of results; 2B+ monthly users |
| **AI Mode** | Google | Custom Gemini with heavy query fan-out (many sub-searches) | Inline links and side panel | Conversational, multi-turn; 1B+ monthly users in 2026 |
| **Perplexity** | Perplexity AI | Fresh web retrieval on every query; its own index, hybrid keyword + vector search, multi-stage reranking | Numbered footnotes on each claim | Built as an answer engine from the start; best citation accuracy in the Tow Center test |
| **ChatGPT search** | OpenAI | Runs multiple web searches per prompt when search is used; architecture not published | Inline source links | Part of a general assistant; search isn't always triggered |

**Why it matters.** All four follow the same basic retrieve-then-generate pattern, but differ in their index, how many searches they run, and how strictly they tie claims to sources. Those choices affect accuracy and which websites get visibility.

---

## 7.6 Limitations and Risks

### Key risks

- **Hallucination despite sources:** misreading, mixing sources, adding details.
- **Wrong or fake citations** and overconfidence (rarely says "I'm not sure").
- **Garbage in, garbage out:** spam, satire or outdated top results.
- **Less traffic for websites** (8% vs 15%) and less diverse views (one summary replaces ten links).
- **Manipulation:** GEO and hidden instructions on pages (Topics 9 and 12).

### Use it well

- Treat the answer as a starting point.
- Open citations for anything important.
- Check each source says what the answer claims.
- Compare with a second source.

### Expanded context from Research Notes

**Hallucination despite sources:** the model can misread a correct page, mix up two sources, or add details no source says.

**Wrong or fake citations:** links that don't support the claim, point to the wrong article, or don't exist.

**Overconfidence:** answers rarely say "I'm not sure," which makes errors hard to spot.

**Garbage in, garbage out:** if the top search results are spam, satire or outdated, the answer inherits the problem.

**Less traffic for websites:** fewer clicks (8% vs. 15% in the Pew study) threaten the publishers whose content the answers rely on, raising fairness and copyright disputes.

**Less diverse views:** one summary replaces ten links, so users see fewer perspectives.

**Manipulation:** "generative engine optimization" and hidden instructions on web pages try to influence what AI search says.

**How to use AI search well:** treat the answer as a starting point, open the citations for anything important, check that each source actually says what the answer claims, and compare with a second source.

---

## Try it yourself

### Activity 7.1 · Be the pipeline (paper)

For "Is it better to visit Japan in spring or autumn for a first trip?" write 5 fan-out sub-queries, then decide which 3 types of source you would cite and why.

**What to notice / answers:** Compare with the example in 7.1: blossom dates, foliage season, crowds, prices, weather.

---

### Activity 7.2 · Citation check (try with an AI search tool)

Ask Perplexity, Google AI Mode or ChatGPT search a recent news question. Open every citation and mark it ✓ supports the claim, ✗ doesn't, or ? broken.

**What to notice / answers:** Work out the share that really supports the claim and compare it with the Tow Center results.

---

## KEY TAKEAWAYS

- 8 steps: understand → fan-out → retrieve → rerank → chunk → generate → cite → check.
- Core tech: RAG, embeddings, hybrid search, reranking, grounding.
- Citations look trustworthy but were wrong 60%+ of the time in the Tow test.

---

## Key terms

| Term | Definition |
|------|------------|
| **Retrieval** | Finding candidate pages or passages for a query. |
| **Reranker** | A second model that re-orders candidates by relevance. |
| **Chunk / passage** | A short section of a page fed to the model. |
| **Grounding** | Basing an answer on supplied sources. |
| **Citation attribution** | Linking each claim to the source it came from. |
| **Hybrid search** | Keyword + vector search combined. |

### Additional key terms (from Research Notes)

| Term | Definition |
|------|------------|
| **Answer engine** | A search tool that writes an answer instead of only listing links. |
| **Query fan-out** | Splitting one question into many sub-searches run in parallel. |
| **Index** | The giant stored copy of web pages a search engine searches. |
| **BM25** | Classic keyword-matching ranking algorithm. |
| **Embedding / vector search** | Matching text by meaning using number vectors. |
| **RAG** | Retrieval-augmented generation: retrieve evidence, then generate. |
| **Zero-click search** | A search where the user gets an answer and clicks nothing. |

---

## Sources (from Research Notes)

1. Nairametrics, AI Overviews hits 2 billion users
2. WrittenlyHub, AI Mode crosses 1 billion users
3. Search Engine Land, Pew study on AI Overview clicks
4. GEO Toolbox, What Is Query Fan-Out?
5. Digiday, WTF is query fan-out
6. ZipTie, How Perplexity AI answers work
7. NIT Agartala, TREC RAG 2025 report (sparse, dense and hybrid retrieval)
8. Canonical/Ubuntu, Hybrid search and reranking
9. WZ-IT, Hybrid search and reranking for RAG
10. Tian Pan, Hybrid Search in Production
11. Columbia Journalism Review / Tow Center, AI Search Has a Citation Problem
12. Nieman Lab, Tow Center study coverage
13. Computing, AI search engines plagued by inaccuracy
14. Idally, error rates by tool
15. Search Engine Land, Pew study (most-cited sites)
16. DEV Community, How Perplexity chooses sources
17. GEO Toolbox, Query fan-out by engine
18. Profound, How to rank in Google AI Mode
19. Geekflare, Perplexity AI glossary
20. Fortune, AI search engines confidently wrong (Tow Center study)
21. Plagiarism Today, AI Search Fails at Citation
22. eMarketer, AI summaries ending search sessions
23. PPC Land, Pew AI summaries study
