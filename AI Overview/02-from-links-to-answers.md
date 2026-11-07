# 02 From Links to Answers

Search went from matching keywords, to understanding questions, to writing the answer itself.

---

## Classic search vs AI search

| | Classic search | AI search |
|---|---|---|
| **You get** | A ranked list of links | A written answer + citations |
| **Who does the reading** | You | The AI |
| **Queries run behind the scenes** | Usually one | Often many ("fan-out") |
| **Follow-up questions** | Start a new search | Continue the conversation |
| **Main risk** | Low-quality pages | Confident but wrong answers |

### Expanded context from Research Notes

An AI search engine (also called an "answer engine") reads the web for you and writes a direct answer with links to its sources, instead of only showing a list of blue links. Main examples: Google AI Overviews and AI Mode, Perplexity, ChatGPT search, Microsoft Copilot and Gemini.

The key difference is not just the output format — it is **who does the work**. In classic search, the engine finds candidate pages, but you must open, read, compare and synthesize them yourself. In AI search, the engine runs many queries behind the scenes (fan-out), retrieves passages, ranks them, and then a language model writes the final answer from those passages. Your role shifts from **reader and comparator** to **verifier of a synthesized answer**.

This matters because the main risk changes: classic search risks wasting your time on low-quality pages, while AI search risks giving you a confident but wrong answer that looks authoritative. As the Research Notes put it, "AI answers can be both impressive and wrong."

---

## How search engines evolved

| Era | What changed |
|-----|--------------|
| **Classic era: keyword matching** | Search engines crawl the web, store pages in an index, and rank the links that contain your words, using formulas such as BM25. |
| **2016 → instant answers** | Weather boxes and featured snippets answer on the results page. About 45% of US Google searches already ended without a click. |
| **2019: understanding** | Google adds BERT (October 2019), which reads the whole query in context. It affected about 1 in 10 US English searches. (See Topic 5 for the Brazil visa example.) |
| **May 2024: AI Overviews** | AI-written summaries roll out to all US Google users. |
| **2026: conversation and agents** | AI Mode passes 1 billion users; assistants start to compare and buy products for you (see Topic 12). |

### Expanded context from Research Notes

**Keyword matching (BM25):** Classic search engines crawl the web, store pages in an index, and rank links that contain your words using formulas like BM25. This era is about **finding pages** — the engine does not understand what you mean, only which pages contain your terms.

**BERT (October 2019):** Google added BERT to Search, affecting about 1 in 10 English searches in the US. BERT reads the whole query in context. The Research Notes give the example: you type "2019 brazil traveler to usa need a visa." Older keyword matching ignored the small word "to" and showed results about US citizens going to Brazil. BERT understands the traveler is going to the USA and returns the right visa page. This was Google's own launch example for BERT.

**AI Overviews (May 2024):** AI-written summaries roll out to all US Google users. This is the moment the engine stops just *finding* and *understanding*, and starts *writing the answer itself*.

**Agents (2026):** AI Mode passes 1 billion users; assistants start to compare and buy products for you. The engine begins to *act* on your behalf.

---

## Zero-click search is rising

A **zero-click search** is one where the user gets what they need on the results page and clicks nothing.

### Share of US Google searches ending with no click

- ~45% (2016)
- 60.45% (2024)
- 68.01% (early 2026)

### Expanded context from Research Notes

The Research Notes provide a detailed table of the traffic shift:

| Measure | Finding | Source |
|---------|---------|--------|
| US Google searches ending with no click | ~45% (2016) → 60.45% (2024) → 68.01% (Jan–Apr 2026) | SparkToro / Similarweb |
| Click rate when an AI summary appears | 8% of visits vs. 15% without one; 1% click a link inside the summary | Pew Research |
| Click-through rate for the #1 result when an AI Overview appears | Down ~58% (Dec 2025), up from a 34.5% drop measured in April 2025 | Ahrefs, 300,000 keywords |
| Lower results also hit | Position 2 lost about half its clicks; position 10 nearly 20% | Ahrefs |
| Google's share of traffic to 75,000+ websites | Down about 22% (June 2025 → May 2026) | Ahrefs tracker via SparkToro |
| Publisher search referrals | Down about 33% globally, 38% in the US, in the year to Nov 2025 | Reuters Institute via Press Gazette |

**Who is hit hardest:** Sites that answer simple informational questions (definitions, how-tos, travel tips, recipes, health facts). Brand and shopping searches are hit less. One Berlin travel guide reported losing 70% of its traffic to AI Overviews after seven years of growth.

**Google's view:** Google argues overall traffic is stable and clicks from AI results are "higher quality," with visitors more likely to stay. Independent studies mostly find fewer clicks.

**Why it matters:** Websites that depend on visits for ad revenue or sales are losing their audience, while AI tools still rely on their content. If creators stop publishing, AI answers have less fresh, reliable material to draw on.

---

## The pattern behind every step

Each step moved more of the work from the user to the search engine:

1. **First finding pages** (keyword search)
2. **Then understanding the question** (BERT)
3. **Now reading and summarizing the sources** (AI Overviews)
4. **Next acting for the user** (agents)

### Expanded context from Research Notes

The Research Notes describe this as a pipeline where each stage takes over more cognitive work:

- **Query understanding:** An LLM works out what you actually want (a fact, a comparison, a how-to, shopping, local results) and rewrites the question into better search terms.
- **Query fan-out:** For complex questions the system splits one question into many sub-questions and searches them all at once. Google says AI Mode "breaks down your question into subtopics and issues a multitude of queries simultaneously."
- **Retrieval:** Each sub-query searches a huge index of web pages, combining keyword search (exact words) with semantic search (matching meaning).
- **Ranking and reranking:** Hundreds of candidate pages are scored for relevance, freshness and trustworthiness.
- **Chunking and context building:** The system pulls out the most useful passages and places them into the LLM's prompt.
- **Generation:** The LLM writes an answer using mainly the supplied passages (retrieval-augmented generation, RAG).
- **Citation attribution:** Claims in the answer are linked to the passage numbers they came from.
- **Checks and display:** Safety filters and quality checks run; the answer is formatted with links, images, tables or follow-up suggestions.

The trajectory is clear: the engine moves from **finding** → **understanding** → **reading and summarizing** → **acting**. Each step shifts more work from human to machine.

---

## Try it yourself

### Activity 2.1 · Timeline card sort (paper)

Write five cards:

1. Keyword matching (BM25)
2. Featured snippets (2016)
3. BERT (2019)
4. AI Overviews (May 2024)
5. Agents (2026)

Shuffle, put them in order, and under each write what work moved from you to the search engine.

**What to notice / answers:** Finding → understanding → reading and summarizing → acting.

---

### Activity 2.1 (continued) · Keywords vs a full question

Search *"visa brazil usa 2019"*, then *"2019 brazil traveler to usa need a visa"*. Compare the top results.

**What to notice / answers:** The small word "to" changes the meaning. This is the BERT example from Topic 5.

---

## KEY TAKEAWAYS

- Classic search: you read; AI search: the AI reads, runs many queries, and writes.
- Timeline: keywords → instant answers (2016) → BERT (2019) → AI Overviews (May 2024) → agents (2026).
- Zero-click searches grew from ~45% to 68%.

---

## Key terms

| Term | Definition |
|------|------------|
| **Index** | The giant stored copy of web pages a search engine searches. |
| **BM25** | Classic keyword-matching ranking algorithm. |
| **Featured snippet** | A quoted answer box shown above the links. |
| **BERT** | Google's 2019 language model that reads queries in context. |
| **Query fan-out** | Splitting one question into many sub-searches run in parallel. |
| **Zero-click search** | A search that ends without clicking any result. |

---

## Sources (from Research Notes)

- SparkToro, In 2026, Less than One Third of Google Searches Still Send a Click
- Search Engine Land, Google zero-click searches hit 68% in early 2026
- Ahrefs, Update: AI Overviews Reduce Clicks by 58%
- PPC Land, Ahrefs position-by-position CTR losses
- Elite Content Marketer, Zero-click statistics (Reuters Institute figures)
- Search Engine Journal, AI Overviews impact on publishers
- Similarweb, Zero-click marketing
- Search Engine Land, Pew study on AI Overview clicks
- TechCrunch, Google brings in BERT to improve its search results
- MobileSyrup, Google Search and conversational queries (BERT)
