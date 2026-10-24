# AI Overview — Module Outline

## 1. Intended Learning Outcomes
By the end of this module, learners should be able to:
1. Understand AI Overviews and explain what they are and why they exist.
2. Explain the fundamentals of AI and how AI Overviews generate answers.
3. Describe the AI search process, from user queries to AI-generated summaries and citations.
4. Use AI Overviews effectively by developing better queries and verifying information.
5. Evaluate answer quality based on accuracy, relevance, completeness, and citation reliability.
6. Identify limitations and failure modes, including hallucinations, outdated information, and misleading answers.
7. Assess user experience by considering usability, trust, accessibility, and inclusivity.
8. Recognize risks and responsibilities, including bias, misinformation, privacy, and publisher impact.
9. Understand the business impact of AI Overviews on search engines, SEO, and online content.
10. Apply the knowledge gained to critically evaluate AI Overviews and make informed decisions about when to trust their answers.

## 2. Prerequisite Knowledge
- Basic computer literacy.
- Ability to read English.
- No prior programming experience is required.

## 3. Table of Contents & Development Status

**Status Labels:** `outline only` | `drafted` | `checked` | `needs revision`

| Section | Topic / Subtopics | Owner | Status | Notes |
|---|---|---|---|---|
| 1 | **AI Overview: The Big Picture** — what AI Overviews are and why they exist | Panha | `outline only` | Needs introductory explanation |
| 2 | **From Links to Answers** — how search evolved to this point | Brain | `outline only` | Focus on SERP evolution |
| 3 | **AI Fundamentals** — What are LLMs? How do they operate? Capabilities? | Kuypheav | `outline only` | Needs terminology definitions |
| 4 | **Who's Playing: The AI Tools People Actually Use** | Kuypheav | `outline only` | Compare ChatGPT, Gemini, Perplexity, etc. |
| 5 | **Under the Hood** — the pipeline from query to cited answer | Pun | `outline only` | Needs a visual flowchart |
| 6 | **Using It Well** — query strategies, verifying claims, when to trust the citations | Brain | `outline only` | Needs a worked example activity |
| 7 | **Making It Accurate** — grounding, hallucination control, source conflicts | Panha | `outline only` | Needs definitions for RAG and grounding |
| 8 | **Measuring Quality** — how you know an overview is good | Egshiglen | `outline only` | |
| 9 | **Limitations & Failure Modes** — When AI gets it wrong | Egshiglen | `outline only` | |
| 10 | **The User Experience** — design, trust signals, edge cases, Accessibility & inclusivity | Shark | `outline only` | |
| 11 | **Risks & Responsibilities** — bias, publishers, misinformation, regulation, privacy, user data | Shark | `outline only` | |
| 12 | **The Business Side** — SEO shifts, monetisation, market dynamics | Pun | `outline only` | |
| 13 | **My Project & Wrap-Up** | [TBD] | `outline only` | |
| 14 | **Conclusion & Takeaways** (10 slides) | [TBD] | `outline only` | |
| 15 | **Key terms** (Glossary: grounding, hallucination, RAG, citation, SERP, etc.) | [TBD] | `outline only` | To be placed at the end of the guide |
| 16 | **Google Form Assessment** (Final version, small knowledge checks every chapter) | [TBD] | `outline only` | Needs questions drafted per chapter |

## 4. Gaps and Uncertainties
- Section 13 ("My Project & Wrap-Up") needs clarification on what the specific project entails.
- We need to decide if the Google Form assessment is created directly in Google Forms or if the questions are drafted in Markdown first.
- Visual assets (flowcharts for Section 5) are missing and need to be created or sourced.

 Chapter 3. LLM Fundamentals

## Learning Objectives

By the end of this chapter, readers should be able to:

1. Explain in plain language what a large language model (LLM) is and what it is fundamentally trained to do.
2. Describe the basic pipeline: tokens → embeddings → transformer/self-attention → next-token prediction.
3. Distinguish pretraining from post-training and explain why an LLM is not the same thing as a product like ChatGPT.
4. Name the main capabilities and the main limitations of LLMs.

---

## Importance of Learning AI Fundamentals

Readers already interact with LLMs through chatbots and AI search features, but the technology often feels like a "black box". Understanding the basic mechanism makes it easier to see why LLMs can write, summarize, translate, and explain — and also why they can confidently produce false statements or lack real-time knowledge.

The underlying system is a statistical next-token predictor operating on numerical representations, not a reasoning engine with access to ground truth.

---

## Key Terms

| Term | Definition |
|---|---|
| **LLM (large language model)** | A neural network trained on massive amounts of text to predict the next token in a sequence. |
| **Token** | A sub-word unit — a word, part of a word, a character, or punctuation — that the model processes as a number. |
| **Embedding** | A numerical representation of a token placed in a multi-dimensional space, so words with similar meanings end up close together. |
| **Transformer** | The neural-network architecture behind most modern LLMs, introduced by Google researchers in 2017. |
| **Self-attention** | The mechanism that lets the model weigh relationships among all tokens in a passage, rather than processing words strictly one by one. |
| **Pretraining** | The first training stage, where the model learns to predict the next token from enormous text corpora. |
| **Post-training** | Later stages — supervised fine-tuning and reinforcement learning from human feedback — that turn a base model into a useful assistant. |
| **Inference** | The process of generating a response one token at a time when a user sends a prompt. |
| **Hallucination / confabulation** | Fluent but factually incorrect output produced by the model. |

---

## What an LLM Is

An LLM is a neural network trained on enormous collections of text — books, articles, websites, and research papers — to process, predict, and generate human language. Its core training objective is simple: **given all the previous tokens, predict the next token.** Through that objective, the model learns language structure and world knowledge encoded in its billions of parameters.

Every model is a parameterized function from token-ID sequences to a distribution over the vocabulary. Training minimizes the divergence between the predicted distribution and the observed next token across the corpus. That is to say, because the objective is distributional, the model is optimized for **plausibility**, not for **verifiability**. It is a closed-book reasoner: everything it "knows" was baked into its weights during training, and the mechanism contains no step that checks a claim against an external source.

Importantly, an LLM is not the same thing as a product like ChatGPT. ChatGPT is a product built on top of an LLM — in OpenAI's case, a GPT model. The useful analogy from Harvard Business School is:

> The LLM is the engine, and the chat application is the vehicle that makes it useful.

---

## How LLMs Operate

LLMs do not process raw text character by character. A tokenizer splits input into tokens, which are sub-word units from a fixed vocabulary. A token might be a full word ("hello"), part of a word ("un" + "believ" + "able"), a single character, or punctuation. Each token maps to a number, and the model operates entirely on those numbers — not on text.

### 1. Tokens and Embeddings

**Tokenization.** The tokenizer choice affects sequence length, out-of-vocabulary behaviour, and how efficiently different languages and scripts are represented. The dominant algorithm is **byte pair encoding (BPE)**. It builds its vocabulary in four steps:

1. Start with a vocabulary containing every individual character (and often bytes, to handle any Unicode).
2. Scan the training corpus and count every adjacent pair of tokens.
3. Merge the most frequent pair into a single new token.
4. Repeat steps 2–3 until the vocabulary reaches a target size.

The result is a vocabulary in which common words are single tokens and rare words are built from pieces. "The" is one token. "Unbelievable" might be "un" + "believ" + "able". Why this shape? Whole-word vocabularies can't handle words the model has never seen, and they would need millions of entries. Character-level vocabularies can build any word, but sequences become very long, and attention cost grows with sequence length. Sub-word vocabularies sit in between: expressive enough for any word, short enough to be efficient.

![Byte pair encoding merges the most frequent adjacent character pairs into sub-word tokens](https://media.geeksforgeeks.org/wp-content/uploads/20260918144115070601/frame_3828.webp)

*Figure 1. Byte pair encoding builds a sub-word vocabulary by repeatedly merging the most frequent adjacent pairs. Image: [GeeksforGeeks — "Byte Pair Encoding (BPE) in NLP"](https://www.geeksforgeeks.org/nlp/byte-pair-encoding-bpe-in-nlp/).*

Two variants do the same job with different merging rules. **WordPiece** is used by BERT and GPT-family models. **SentencePiece** works directly on raw text and handles languages without spaces, such as Chinese and Japanese. Vocabulary size matters as well: Llama 3 uses a 128K-token vocabulary. A bigger vocabulary shortens sequences but makes the output layer more expensive; a smaller one does the reverse.

The output of tokenization is a list of integer IDs. From this point on, the model never sees text — only numbers.

**Embeddings.** Each token is transformed into a numerical representation called a word embedding. Think of it as placing each token in a multi-dimensional space: words with similar meanings end up close together, which helps the model understand context and relationships.

Each token ID is used to look up a row in a large table — the embedding matrix. That row is a vector of, say, 4,096 numbers. This replaces **one-hot encoding**, in which each word gets a vector of all zeros with a single 1. One-hot can't express similarity at all, because every pair of words is exactly as far apart as every other pair.

In an embedding space, distance means something. Words used in similar contexts end up with similar vectors, because training nudges them there. You can add and subtract them: the classic example is that "king" − "man" + "woman" lands near "queen."

There are two kinds of embeddings. Word2Vec and GloVe gave each word one fixed vector regardless of context. Transformers do not. Because attention mixes in information from the surrounding words, "bank" in "river bank" and "bank" in "investment bank" end up with different vectors. The vector is contextual — it depends on the whole sentence.

![Embedding space in which words with similar meanings are positioned close together](https://matthewmanela.com/wp-content/uploads/2023/10/image-3.png)

*Figure 2. Embeddings represent tokens as vectors in a multi-dimensional space, where proximity encodes similarity of meaning. Image: [Matthew Manela — "Exploring the Power of LLM Embeddings"](https://matthewmanela.com/blog/exploring-the-power-of-llm-embeddings/).*

### 2. The Transformer and Self-Attention

This is the part that does the actual thinking. Imagine a room where every word in your sentence can look at every other word and decide which ones are relevant to it.

Take the sentence: *"The animal didn't cross the street because it was too tired."* What does "it" refer to? You know it's the animal, not the street. A model with attention can work that out too: when processing "it", it looks back at all the other words, decides "animal" is the most relevant one, and pulls that meaning in.

The model does this in many layers, stacked on top of each other. Each layer lets words refine their understanding using what the previous layer worked out. Because a stack of layers has no sense of order, the model also needs seat numbers — that's what **positional encoding** does, so it knows which word came first.

![Positional encoding adds a position signal to each token embedding](https://media.geeksforgeeks.org/wp-content/uploads/20250818131508982635/positional_encoding_in_transformer.webp)

*Figure 3. Positional encoding injects a position signal into each token's embedding, so the model can tell "dog bites man" from "man bites dog". Image: [GeeksforGeeks — "Positional Encoding in Transformers"](https://www.geeksforgeeks.org/nlp/positional-encoding-in-transformers/).*

Every token in the input has a list of numbers attached to it — its vector. That vector is the model's current best guess at what that token means in this sentence. Self-attention is the operation that lets each token revise its vector by looking at the other tokens around it. The process happens in five steps.

**Step 1 — Three projections.** For each token's vector, the model computes three new vectors by multiplying it against three different learned weight matrices:

| Vector | Role |
|---|---|
| **Query** | "What kind of information am I looking for?" |
| **Key** | "What kind of information do I offer?" |
| **Value** | "What information do I actually carry?" |

The names are a useful metaphor, not a literal description. Concretely, they are just three linear transformations of the same input vector.

![The same input vector projected three ways into query, key, and value vectors](https://miro.medium.com/v2/resize:fit:1200/1*6JpXMLrsmNcf8-x3aV2Tvg.png)

*Figure 4. One input vector is projected three ways — query, key, and value — using three separately learned weight matrices. Image: [2020 Machine Learning — "Decoding the Key, Query, Value Mechanism in Transformer Models"](https://2020machinelearning.medium.com/decoding-the-key-query-value-mechanism-in-transformer-models-thru-a-deep-discussion-with-claude-ai-2da5a66d4f8e).*

**Step 2 — Scoring.** To decide how much token A should pay attention to token B, the model takes the dot product of A's query with B's key. A dot product measures alignment: if the two vectors point in similar directions, the result is large and positive; if they are unrelated or opposed, it is small or negative. So a high score means "B's key matches what A's query is looking for."

The model does this for every ordered pair of tokens. With *n* tokens, that is *n* × *n* scores.

**Step 3 — Why the √d_k.** *d_k* is the length of that list of numbers (the key dimension). Before using the scores, they are divided by the square root of the key dimension. Here is the reason: a dot product of two long vectors sums many terms, so its magnitude grows with the vector length. Feed very large numbers into a softmax and it saturates — one weight becomes close to 1 and the rest close to 0, so the model attends to exactly one token and ignores the rest, and the gradient through that operation nearly vanishes, which stalls learning. Dividing by √d_k keeps the scores in a range where the softmax stays smooth, scaling the numbers back to a normal size to avoid saturation.

**Step 4 — Turning scores into weights.** A **softmax** is applied across each row. Softmax converts a list of arbitrary numbers into a list of positive numbers that sum to 1 — a set of shares. So after this step, token A has a distribution over all tokens: "I'm giving 40% of my attention to *animal*, 5% to *street*, and so on."

**Step 5 — Mixing.** A's new vector is the weighted sum of all the value vectors, using those shares as weights. If A decided *animal* matters most, A's representation absorbs mostly *animal*'s value vector. That is the whole operation: each token's new meaning is a blend of the meanings of the tokens it decided were relevant.

**Causal masking.** For a model that generates text left to right, token 5 must not be allowed to look at token 6 — token 6 does not exist yet at generation time, and training on it would be cheating. This is the **causal mask**, and it is what makes left-to-right generation well-defined.

![A causal mask blocks each token from attending to future positions](https://llm.modular.com/images/causal-masking-light.png)

*Figure 5. The causal mask zeroes out attention to future tokens, so token 5 can see tokens 1–5 but not token 6. Image: [Modular — "LLM Step 03"](https://llm.modular.com/step_03.html).*

Most modern LLMs are built on the transformer architecture. Earlier language models processed text more sequentially, which made it hard to capture relationships across long passages. Transformers use self-attention to consider relationships among words throughout an entire sentence, paragraph, or document. More technically, self-attention computes, for each token, a weighted combination of representations of every other token in the context, with weights derived from learned query, key, and value projections. This is why transformers can handle long-range context and why training can be parallelized efficiently across accelerators.

### 3. Training: Pretraining → Post-Training → Reasoning

Modern LLMs go through multiple training stages.

![A pipeline of the training stages an LLM passes through](https://github.com/user-attachments/assets/5bfae9c4-9fea-472c-ac15-271479c0e1e3)

*Figure 6. Modern LLMs are trained in stages — pretraining, post-training, and reasoning-focused reinforcement learning — each with a different training signal. Image: [Intelligent Tools — "Demystifying Large Language Models"](https://intelligenttools.co/blog/demystifying-large-language-models).*

| Stage | Objective | What it produces |
|---|---|---|
| **1. Pretraining** | Next-token prediction over a large corpus | A base model: good at continuing text, bad at being an assistant |
| **2. Post-training (SFT + RLHF)** | Instruction-following and human-preferred behaviour | An assistant |
| **3. RLVR** (reasoning models) | Correct final answers in checkable domains | A reasoning model |

**Stage 1 — Pretraining.** The training signal comes free with the data, because the correct answer is simply the next word in the text. Run this over a large corpus and the model is forced to learn syntax, vocabulary, factual associations, and a great deal of world structure, because all of those are useful for predicting what comes next.

What comes out is a **base model**. It is very good at continuing text and very bad at being an assistant. Ask it a question and it may answer, or it may continue with more questions, because both are plausible continuations of a document that happens to contain a question. It has never been told that the desired behaviour is "respond helpfully to the user."

**Stage 2 — Post-training.** This turns a base model into a useful assistant through **supervised fine-tuning (SFT)** and **reinforcement learning from human feedback (RLHF)**.

- **SFT** trains the model on curated examples of helpful assistant behavior. First, the model is shown many examples of good question-and-answer pairs, so it learns the shape of a helpful reply.
- **RLHF** then uses human preference comparisons to tune the model toward responses people prefer. Humans rank pairs of answers — "which of these two is better?" — and the model learns to lean toward the ones people prefer. This is where it learns tone, brevity, and when to hedge.

> Ever used ChatGPT and suddenly it asks you to pick a response? This is the training in action.

**Stage 3 — Reinforcement learning with verifiable rewards (RLVR).** For maths and code, there is a better signal than human preference: whether the answer is actually correct. A maths answer can be checked against the known solution; a program can be run against test cases. So the reward does not come from a learned model of human taste — it comes from an automatic checker.

The training loop is:

1. The model generates a reasoning trace and a final answer.
2. The checker verifies the final answer.
3. The model is rewarded or penalized accordingly.

Crucially, the reasoning trace itself is not scored — it is stripped before checking. The model is free to reason however it likes, and is rewarded only for reaching correct conclusions.

This is what produces the behaviour people call "reasoning." The model learns that generating intermediate steps improves its odds of a correct final answer, because that is what the reward signal selects for.

> **Caveat:** RLVR works because maths and code have checkers. Most real questions do not. Reasoning gains in verifiable domains have not reliably transferred to open-ended reasoning, and that is an open research problem rather than a solved one.

### 4. Inference: Generating One Token at a Time

When you send a request, the model generates its response through **autoregressive generation**. When you send a message, the model writes its reply one word at a time. It looks at everything so far — your message plus whatever it has already written — and picks the most likely next word. Then it adds that word and does it again. And again, until it decides to stop.

Your full prompt is converted into tokens and fed into the model. The model produces a probability distribution over its vocabulary — predicting which token is most likely to come next. A token is selected, appended to the sequence, and the updated sequence is fed back in to generate the next token. This repeats until a stop token or length limit is reached.

Two things follow from this.

**First, the model can only see what fits on its desk.** Everything — your question, any documents pasted in, and the answer being written — has to fit inside what's called the **context window**. When people say a model has a "1 million token context window", they mean the desk is that big. It's big, but it's still a desk. Modern models offer context windows from 4K to over 1M tokens, but the window is always finite.

**Second, it's not perfectly repeatable.** Because the model is picking from a range of likely words rather than always taking the single most likely one, the same question can get slightly different answers on different days. Set the randomness to zero and it's more repeatable, but not guaranteed bit-for-bit identical across different machines.

---

## What LLMs Are Good At

LLMs excel at language understanding and generation. Sourced capabilities include:

| Capability | What it looks like |
|---|---|
| **Reasoning and analysis** | Breaking down problems, comparing options, explaining concepts. |
| **Content generation** | Writing articles, emails, reports, and code. |
| **Summarization** | Distilling long documents into key points. |
| **Translation** | Converting between natural languages or formats. |
| **Code generation** | Writing, explaining, and debugging code. |
| **Classification and extraction** | Categorizing text and extracting structured data. |
| **Multimodal understanding** | Many modern LLMs can process images, audio, and video alongside text. |
| **Structured output** | Generating precise formats like JSON or XML. |

At a practical level, LLMs can hold conversations, summarize reports, draft emails, and explain complex topics in simple terms.

---

## What LLMs Struggle With

Understanding limitations is critical for using LLMs well. Sourced limitations include:

| Limitation | What it means |
|---|---|
| **No real-time knowledge** | Training data has a cutoff date; the model does not know about events after training. |
| **Hallucinations** | LLMs can generate confident but factually incorrect responses. They produce plausible-sounding text rather than retrieving verified facts. The IEEE describes this as "confabulation" — fluent but false statements — and notes it is a persistent failure mode. |
| **No persistent memory** | Each API call is stateless; the model does not remember previous conversations unless they are included in the context window. |
| **Limited math and logic** | While improving, LLMs can make errors in precise calculations and formal logic. |
| **Non-determinism** | The same prompt can produce different responses across calls. |
| **No ability to act on its own** | LLMs generate text; they cannot send emails, query databases, or call APIs without tooling. |

---

## Worked Example: Why an LLM Alone Is Not a Search Engine

A plain LLM answers from patterns learned during training. If you ask about something recent, it may not know, or it may hallucinate. That is why AI search products add retrieval: they fetch documents at query time and ground the answer in those documents rather than relying only on the model's parameters.

This distinction is the bridge to Chapter 4.

---

## Chapter Recap

- An LLM is a next-token predictor trained on massive text data.
- It works with tokens and embeddings, and uses transformer self-attention to model relationships across text.
- Training has stages: pretraining, post-training (SFT + RLHF), and sometimes reasoning-focused reinforcement learning.
- LLMs are strong at language tasks but weak on real-time knowledge, factual verification, persistent memory, and precise logic.
- An LLM is an engine; a product like ChatGPT is a vehicle built around it.

---

## Knowledge Check

**1. Recall.** What is an LLM's core training objective?

**2. Application.** Why might an LLM confidently answer a question about a recent event incorrectly?

**3. Compare.** What is the difference between pretraining and post-training?

**4. Evaluate.** A chatbot gives a fluent, well-structured answer with no sources. Why should you not automatically trust it?

---

### Answers

#### 1. Recall — Core training objective

**Model answer.** Next-token prediction. Given all the previous tokens, the model predicts a probability distribution over the next token, and training adjusts the weights so that the observed next token in the corpus becomes more likely. The objective is plausibility, not truth.

**Must contain:**

- "Predict the next token/word" as the core objective
- Recognition that this is a statistical objective, not a truthfulness or helpfulness objective

#### 2. Application — Confident answers about recent events

**Model answer.** Two mechanisms combine. First, **training cutoff**: if the event happens after the model's training data ends, the model has no parametric knowledge of it at all. Second, **no truthfulness signal**: the model generates the most plausible continuation, and a fluent, confident-sounding answer is a plausible continuation whether or not the content is true. It has no internal step that distinguishes "I remember this" from "this sounds like it should be true." Confidence in the output reflects fluency of the text, not certainty of the model.

**Must contain:**

- The cutoff explaining *why it doesn't know*
- The mechanism explaining *why it sounds confident anyway*
- The distinction between fluent and correct

#### 3. Compare — Pretraining vs. post-training

**Model answer.** They have different objectives and produce different artifacts.

**Pretraining** is self-supervised next-token prediction over a large corpus. It teaches language structure and world knowledge, because those are useful for predicting what comes next. The output is a **base model** — good at continuing text, bad at being an assistant. It has no concept that a question should be met with a helpful answer.

**Post-training** is a set of later stages that shape behaviour:

- **SFT** on curated prompt–response pairs — teaches format and instruction-following
- **RLHF** — trains a reward model on human preference rankings, then optimizes the language model against it; teaches judgement, tone, hedging
- **RLVR** (reasoning models) — rewards correct final answers in checkable domains like maths and code

The short version: **pretraining teaches the model language; post-training teaches it manners.**

**Must contain:**

- Different objectives (next-token vs. behaviour shaping)
- Different outputs (base model vs. deployed assistant)
- At least the SFT/RLHF distinction within post-training

#### 4. Evaluate — Why not automatically trust a fluent, sourced answer

**Model answer.** Three independent reasons.

**Fluency is not evidence.** The model is optimized to produce plausible next tokens. A fluent, well-structured answer is exactly what that mechanism produces, whether the content is true or invented. Structure and tone carry no information about correctness — they are properties of the text distribution, not of the facts.

**There is no verification path.** With no sources, there is nothing to check the claims against. You cannot distinguish a claim drawn from a retrieved document from one the model generated to fill a gap. (Compare Chapter 4: even with citations, the source shows what the model used, not that it used it correctly — but without citations, you have not even that.)

**Confidence is not a signal either.** The absence of hedging tells you nothing, because "I don't know" is a trained behaviour, not a default. A model that has not been specifically taught to express uncertainty will produce a confident answer rather than admit a gap.

**Must contain:**

- Fluency/structure ≠ truth
- No sources = no independent check
- Confident tone ≠ model certainty

---

## References

*All statistics and claims retrieved October 21, 2026. This field changes monthly; date-check any figure before publication.*

1. Microsoft Learn. LLM fundamentals. Microsoft Learn. Accessed October 21, 2026. https://learn.microsoft.com/en-us/agent-framework/journey/llm-fundamentals

2. Harvard Business School Online. What are large language models (LLMs) & how do they work? Harvard Business School Online. Accessed October 21, 2026. https://online.hbs.edu/blog/post/what-are-llms

3. IEEE Technology Navigator. Large language models. IEEE. Accessed October 21, 2026. https://technav.ieee.org/topic/large-language-models/

4. The evolution of AI: from classical machine learning to modern large language models. IEEE Xplore. Accessed October 21, 2026. https://ieeexplore.ieee.org/abstract/document/11202920

5. A web-based solution for federated learning with LLM-based automation. IEEE Xplore. Accessed October 21, 2026. https://ieeexplore.ieee.org/document/10891639

6. Language models that think, chat better. arXiv. Preprint posted 2025. Accessed October 21, 2026. https://arxiv.org/abs/2509.20357

7. The when where and how of LLM failures, measured. Zenodo. Accessed October 21, 2026. https://zenodo.org/records/14243944

8. Tree of agents: improving long-context capabilities of LLMs. In: *Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics*. Association for Computational Linguistics; 2025. Accessed October 21, 2026. https://aclanthology.org/2025.acl-long.1012/

9. GeeksforGeeks. Byte pair encoding (BPE) in NLP. Accessed October 21, 2026. https://www.geeksforgeeks.org/nlp/byte-pair-encoding-bpe-in-nlp/

10. Manela M. Exploring the power of LLM embeddings. Matthew Manela. Accessed October 21, 2026. https://matthewmanela.com/blog/exploring-the-power-of-llm-embeddings/

11. GeeksforGeeks. Positional encoding in transformers. Accessed October 21, 2026. https://www.geeksforgeeks.org/nlp/positional-encoding-in-transformers/

12. 2020 Machine Learning. Decoding the key, query, value mechanism in transformer models thru a deep discussion with Claude AI. Medium. Accessed October 21, 2026. https://2020machinelearning.medium.com/decoding-the-key-query-value-mechanism-in-transformer-models-thru-a-deep-discussion-with-claude-ai-2da5a66d4f8e

13. Modular. LLM Step 03: causal masking. Accessed October 21, 2026. https://llm.modular.com/step_03.html

14. Intelligent Tools. Demystifying large language models. Accessed October 21, 2026. https://intelligenttools.co/blog/demystifying-large-language-models

# Topic 5: Under the Hood
How AI search turns a question into a cited answer

**The pipeline at a glance:** query fan-out → retrieval and indexes → reranking and passage selection → grounding and generation (RAG) → citation attribution. Platform differences (6) and accuracy and failure modes (7) apply to every step.

## 5.1 Query fan-out

**In simple terms:** The AI doesn’t search once. It splits your question into many smaller questions and searches each, like asking five friends five different things to answer one big question.

**What it is:** Query fan-out is when an AI search system breaks a question into several smaller searches to gather information from different angles.

**How it works**

- The system identifies the main question and related subtopics.
- It generates multiple search queries, sometimes running them in parallel.
- It gathers the results and combines relevant information into one response.

**Why it matters:** A website might not rank for the user’s original question but can still appear for one of the smaller searches.

**Business impact:** Companies need useful content covering specific customer questions, not just one page aimed at a popular keyword.

**Example:** “What is the best electric car for a university student?” might become separate searches on prices, battery range, safety ratings and charging costs.

**Research findings**

Google says AI Overviews and AI Mode may use this “query fan-out” technique.
AI prompts are long, around 70 to 80 words versus 3 to 4 for traditional queries.
AirOps (a vendor) found 88.6% of ChatGPT prompts produce exactly two sub-queries, and 95% of those have zero search volume. Informational queries are often restated near-verbatim (39.9%), while commercial ones are often split into components (38.4%).
32.9% of citations came only from fan-out results, never the original prompt’s results.

**Sources**

- Google Search Central, AI features: https://developers.google.com/search/docs/appearance/ai-features
- Google, AI Mode update: https://blog.google/products-and-platforms/products/search/google-search-ai-mode-update/
- GEO Toolbox, “What is query fan-out”: https://geotoolbox.ai/blog/query-fan-out
- AirOps, “Query fan-out pipeline”: https://www.airops.com/blog/query-fanout-pipeline
## 5.2 Retrieval and indexes

**In simple terms:** An index is a giant catalogue of web pages, like a library’s. The AI searches the catalogue to find pages that might help. If your page isn’t in it, the AI can’t find it.

**What it is:** Retrieval is finding relevant information. An index is a structured database that lets a search engine find web content efficiently.

**How it works**

- Search engines discover and crawl web pages.
- They process the content and store it in searchable indexes.
- When a question arrives, the system retrieves potentially relevant pages or passages.
- Some AI systems also use licensed databases, product catalogues or connected tools.

**Why it matters:** A page that isn’t indexed or accessible is less likely to appear in answers, but being indexed doesn’t guarantee selection.

**Business impact:** Sites need to be technically accessible, clearly structured and useful so systems can discover them.

**Example:** A shop’s product page that blocks crawlers may never be retrieved, however good it is.

**Research findings**

Retrieval often uses hybrid retrieval merged with reciprocal rank fusion (RRF). Hybrid search combines vector search with traditional keyword search for better recall.
Embeddings capture meaning, not keywords, so differently worded text can still match.
One analysis says ChatGPT pulls about 36.5 pages per query but cites only around 15%.
Retrieval isn’t the same as top rankings: only 38% of AI Overview citations come from the top 10 organic results.
One vendor guide ties ChatGPT’s retrieval to Bing (via Bing integration), but that is vendor-reported.
Blocking isn’t airtight: TollBit found 15% of AI page fetchers in Europe reached URLs that had been disallowed.

**Sources**

Google Search Central, How Search Works (named in your ChatGPT document; I haven’t opened it)
- Peec, “How AI search chooses passages”: https://docs.peec.ai/research/how-ai-search-chooses-passages
- Parse, “How AI retrieval works”: https://www.parse.gl/blog/how-ai-retrieval-works-brands
- Vizup: https://www.tryvizup.com/blog/how-ai-search-engines-retrieve-and-cite-content
- Averi (Bing claim): https://www.averi.ai/learn/the-definitive-guide-to-geo-get-cited-by-ai-in-2026
- PPC Land, crawl-to-referral ratio (TollBit finding): https://ppc.land/crawl-to-referral-ratio/
## 5.3 Reranking and passage selection

**In simple terms:** The AI grabs a big pile of possible answers, then keeps only the best few, like picking your top 5 candies from a bowl of 150. It judges small pieces (single paragraphs), not whole pages.

**What it is:** After retrieving many sources, the system scores and reorders them. Passage selection means choosing specific sections rather than the whole page.

**How it works**

- The system retrieves a broad set of candidates.
- A ranking model evaluates how closely each matches the question.
- It selects useful passages or paragraphs for the answer.

**Why it matters:** A site with excellent information can still be overlooked if the relevant detail is unclear or hard to find.

**Business impact:** Clear headings, direct answers, accurate facts and organised information can help, but there is no guaranteed formula for being selected.

**Example:** For “does this electric car perform well in cold weather?”, a paragraph on winter battery performance beats a general introduction.

**Research findings**

A cross-encoder-style model reads each candidate passage against the query and re-scores the shortlist.
Chunking decides what the model sees, and overlapping chunks help preserve context at the edges.
In one analysis, position 1 was cited 58% of the time, position 5 about 25%, and position 10 only 14%.

**Sources**

- Peec: https://docs.peec.ai/research/how-ai-search-chooses-passages
- AirOps: https://www.airops.com/blog/query-fanout-pipeline
- Glukhov, RAG guides: https://www.glukhov.org/categories/rag/
- Dotzlaw: https://dotzlaw.com/insights/retrieval-augmented-generation-grounding-ai-with-real-world-knowledge/
Nogueira and Cho, Passage Re-ranking with BERT (named in your ChatGPT document; I haven’t opened it)
## 5.4 Grounding and generation (RAG)

**In simple terms:** Grounding means the AI checks real sources while answering instead of guessing from memory, like writing a school report with the books open beside you.

**What it is:** Grounding connects an answer to evidence. RAG (retrieval-augmented generation) retrieves outside information and hands it to a language model when it writes the answer.

**How it works**

- The user asks a question.
- The system retrieves relevant documents or passages.
- The model uses them as context.
- The model writes an answer from the question and the evidence.

**Why it matters:** Evidence can make answers more current and checkable, but retrieval doesn’t guarantee correctness: sources can be outdated or contradictory, and the model can misread them.

**Business impact:** Companies with accurate, current, accessible information are likelier to be represented correctly.

**Example:** For “latest price of this laptop”, the system can fetch the retailer’s current page rather than rely on training data.

**Research findings**

Models have a knowledge cutoff and a finite context window, so RAG looks up the relevant information first and puts it into the prompt.
Grounding is using retrieved information to support the claims in the response, which differs from indexing. Synthesis composes one answer from sources that may not fully agree.
Components include a chunker, an embedding model, a vector database and a generator (the LLM that produces the final response from the augmented prompt).
One practitioner write-up says models attend most to the beginning and end of context, with a “lost in the middle” effect. That’s a single blog’s summary, so verify it.

**Sources**

Lewis et al. (2020), Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks (named in your ChatGPT document; I haven’t opened it)
- NovCog, “RAG Fundamentals”: https://gist.github.com/NovCog/626815a4fbd4c8c6a22d50a421b90d31
- Airtribe: https://www.airtribe.live/upskill-for-free/resources/interactive-explainers/grounding/grounding-your-data
- AI Agent Design Patterns wiki: https://github.com/joehubert/ai-agent-design-patterns/wiki/Retrieval%E2%80%90Augmented-Generation-(RAG)
- Vizup: https://www.tryvizup.com/blog/how-ai-search-engines-retrieve-and-cite-content
## 5.5 Citation attribution

**In simple terms:** The AI adds “I got this from here” links, like footnotes. Sometimes a brand is mentioned in the answer without getting a link.

**What it is:** Linking claims in an answer to the sources that support them. Two ideas to keep apart:

- Citation: the answer includes a link.
- Attribution: the source really supports that claim. A link alone doesn’t prove it does.

**How it works:** The system selects sources, decides which claim each supports, and renders links or footnotes. Formats vary by platform.

**Why it matters:** Users need to verify information, and publishers want credit and visitors.

**Business impact:** A company can be mentioned without a clickable link, so brand visibility and website traffic can come apart.

**Example:** An answer says a laptop has the longest battery life and links a review. To check attribution, open the review and see whether it makes that comparison.

**Research findings**

The Tow Center (March 2025) tested eight AI search tools on news citations and they got the information wrong more than 60% of the time. Perplexity was wrong 37% of the time and Grok-3 94%.
The tools fabricated links and cited syndicated copies, and licensing deals didn’t guarantee accurate citation.
32.9% of citations came only from fan-out results, so the cited page may never have appeared for the original question.

**Sources**

- Nieman Lab on the Tow Center study: https://www.niemanlab.org/2025/03/ai-search-engines-fail-to-produce-accurate-citations-in-over-60-of-tests-according-to-new-tow-center-study/
- Fortune via Yahoo: https://tech.yahoo.com/ai/articles/ai-search-engines-confidently-wrong-122456267.html
Columbia Journalism Review, “AI search has a citation problem” (original study)
OpenAI Help Center, “Searching the web with ChatGPT” and Perplexity Help Center, Pro Search (named in your ChatGPT document; I haven’t opened them)
## 5.6 Platform differences

**In simple terms:** Each AI search tool is a different chef making the same dish with a different recipe, so ChatGPT, Google and Perplexity often pick different sources.

**What it is:** Different platforms can give different answers and cite different sites for the same question.

**How it works:** Platforms may differ in their search providers and sources, how they expand queries, how they rank and select, the models and instructions that write the answer, and their citation formats.

**Why it matters:** Appearing in one platform’s answer doesn’t mean appearing in another’s.

**Business impact:** Businesses may need to monitor visibility across several platforms, not just Google rankings.

**Example:** “Best universities for mechanical engineering in Europe” may draw on different rankings, official pages and education sites in each tool.

**Research findings**

Google documents fan-out. For others it’s inferred: ChatGPT runs multiple searches per prompt, but OpenAI hasn’t published the retrieval architecture, and Perplexity’s behaviour matches the pattern but isn’t clearly vendor-labeled.
Citation habits differ. Vendor guides report Reddit is 46.7% of Perplexity’s top-10 citations and 21% of Google AI Overview citations. Those are unverified vendor numbers.
Error rates varied widely in the Tow Center test (Perplexity 37%, Grok-3 94%), per 5.5.
None of these sources shows which platform is best overall.

**Sources**

- GEO Toolbox: https://geotoolbox.ai/blog/query-fan-out
- RankAI: https://rankai.ai/articles/how-to-do-geo
- Nieman Lab: https://www.niemanlab.org/2025/03/ai-search-engines-fail-to-produce-accurate-citations-in-over-60-of-tests-according-to-new-tow-center-study/
Google, OpenAI web search documentation and Perplexity “How it works” (named in your ChatGPT document; I haven’t opened them)
## 5.7 Accuracy and failure modes

**In simple terms:** The AI sometimes gets it wrong and says it with total confidence. It might link a page that doesn’t exist or credit the wrong site, like a kid who’s sure of the answer but mixed up the facts.

**What it is:** AI search can state false information, misread sources, or cite sources that don’t support the claim.

**Common failure modes**

- Hallucination: false or unsupported information.
- Outdated information: old facts used after things changed.
- Incorrect attribution: a claim linked to a source that doesn’t support it.
- Source selection errors: low-quality or misleading material relied on.
- Conflicting evidence: disagreeing sources merged without explanation.

**Why it matters:** Answers sound confident even when wrong. Citations make checking easier but don’t remove errors.

**Business impact:** Wrong AI statements can hurt a company’s reputation and mislead customers, so keep key web information accurate and current.

**Example:** An assistant recommends a university using an outdated tuition fee, or misstates an admission requirement from an old page.

**Research findings**

Each pipeline stage fails differently, so a page can be missed at fan-out, retrieval or reranking.
Tools were also confidently wrong, and got the information wrong more than 60% of the time in the Tow Center news-citation test.
Your ChatGPT document cites a 2025 medical-referencing study (60.4% of 303 references accurate; 22.2% of 451 citations highly relevant). I haven’t verified it, and the document itself says it shouldn’t be generalised. Check it on PubMed, or lean on the Tow Center results, which are about AI search.

**Sources**

- Nieman Lab: https://www.niemanlab.org/2025/03/ai-search-engines-fail-to-produce-accurate-citations-in-over-60-of-tests/
- Fortune via Yahoo: https://tech.yahoo.com/ai/articles/ai-search-engines-confidently-wrong-122456267.html
- Peec: https://docs.peec.ai/research/how-ai-search-chooses-passages
2025 medical-referencing study on PubMed (linked in your ChatGPT document)
## How the Seven Topics Connect
Query fan-out: break the question into smaller searches.
Retrieval and indexes: find relevant pages and information.
Reranking and passage selection: pick the most useful sources and passages.
Grounding and generation: use that evidence to write the response.
Citation attribution: connect claims to supporting sources.
Platform differences: each tool runs its own version of steps 1 to 5.
Accuracy and failure modes: things can go wrong at every step, so users must check.

# Chapter 8: Measuring Quality

## 1. Learning Objectives

By the end of this chapter, students will be able to:

1. Explain why Google AI Overviews (AIOs) need to be evaluated.
2. Identify five key quality criteria.
3. Apply these criteria to an AI Overview.
4. Describe methods and metrics used to measure quality.
5. Evaluate an AI Overview using a practical example.

## 2. Introduction

Google AI Overviews provide AI-generated summaries in search results. They can help users find information quickly, but a clear and confident answer is not always accurate, complete, or well-supported.

Therefore, evaluating an AI Overview involves more than checking whether the answer sounds correct. Users must examine its accuracy, relevance, completeness, source quality, and citation quality.

## 3. Key Terms

- **Accuracy:** Whether the information is factually correct.
- **Relevance:** Whether the answer addresses the user’s question.
- **Completeness:** Whether the answer includes the essential information needed.
- **Source Quality:** How reliable and trustworthy the cited sources are.
- **Citation Quality:** Whether citations genuinely support the claims they accompany.
- **Evaluation Criteria:** The standards used to judge answer quality.
- **Evaluation Metrics:** Measurable indicators used to assess specific aspects of quality.

## 4. Main Explanation

### 4.1 Accuracy

Accuracy measures whether the information in an AI Overview is factually correct. An answer may sound convincing while containing incorrect dates, numbers, definitions, or explanations.

**Example:** An AI Overview gives the wrong year for a historical event.

**Why it matters:** Incorrect information can mislead users, even when the answer is written confidently.

### 4.2 Relevance

Relevance measures how well an AI Overview answers the user’s actual question. A response may contain correct information but still fail to address the user’s intent.

**Example:** A user asks about the health benefits of walking, but the answer mainly discusses running.

**Why it matters:** A useful answer must address the question the user intended to ask.

### 4.3 Completeness

Completeness measures whether an answer includes the essential information needed to understand a topic. A short summary does not need to include every detail, but it should not omit important facts or qualifications.

**Example:** An answer explains the benefits of a medication but leaves out important risks or warnings.

**Why it matters:** Missing information can create a misleading impression even when the statements included are correct.

### 4.4 Source Quality

Source quality concerns the reliability of the websites and documents used to support an AI Overview. Reliable sources may include official organizations, academic research, and recognized subject experts, depending on the topic.

**Example:** An answer about public health relies on an anonymous blog instead of relevant medical guidance.

**Why it matters:** Weak or unsuitable sources reduce confidence in the information presented.

### 4.5 Citation Quality

Citation quality measures whether the cited sources actually support the claims in an AI Overview. A reliable website is not enough if it does not provide evidence for the specific statement being made.

**Example:** An AI Overview cites a scientific article, but the article does not support the numerical claim beside the citation.

**Why it matters:** Users should check both the reliability of a source and whether it supports the particular claim.

### 4.6 Evaluation Methods and Metrics

Evaluation methods are the procedures used to assess an AI Overview, while metrics help measure particular aspects of its quality.

Common methods include:

1. **Claim-by-claim verification:** Check individual statements against reliable sources.
2. **Relevance and completeness checks:** Determine whether the answer addresses the question and includes essential information.
3. **Source and citation auditing:** Open cited sources and verify whether they support the claims.
4. **Quantitative evaluation:** Calculate simple metrics to summarize the results.

Two useful metrics are:

**Observed Accuracy Rate**

$$
\\text{Observed Accuracy Rate} =
\\frac{\\text{Claims verified as correct}}{\\text{Claims checked}} \\times 100\\%
$$

**Claim-Support Rate**

$$
\\text{Claim-Support Rate} =
\\frac{\\text{Claims supported by cited sources}}{\\text{Claims checked}} \\times 100\\%
$$

**Example:** Suppose an evaluator checks 10 claims. Eight are factually correct, while seven are supported by their cited sources.

- Observed Accuracy Rate = (8/10) × 100% = **80%**
- Claim-Support Rate = (7/10) × 100% = **70%**

These results measure different things: a claim may be correct but not adequately supported by its citation.

**Key point:** No single metric captures every aspect of answer quality. Qualitative checks and quantitative measurements should be used together.

### 4.7 Real-World Evaluation

To evaluate a real Google AI Overview, follow these steps:

1. **Choose a query:** Search a clear question on Google.
2. **Record the answer:** Note the main claims made in the AI Overview.
3. **Check accuracy:** Verify factual statements using reliable sources.
4. **Assess relevance and completeness:** Decide whether the answer addresses the question and includes essential details.
5. **Review sources and citations:** Check the credibility of the sources and whether they support the claims.
6. **Summarize the results:** Record strengths, weaknesses, and an overall assessment.

The evaluation should be based on the answer and sources actually observed, rather than assumptions about how AI Overviews usually perform.

## 5. Practical Case Study

### Evaluating an AI Overview About Coffee

**Query:** “What are the benefits and risks of drinking coffee?”

Search this query on Google and examine the AI Overview if one appears. Use the table below to evaluate the actual answer. Do not assume that an AI Overview will appear or that it will contain a particular claim.

| Evaluation Criterion | Questions to Consider | Your Findings |
|---|---|---|
| Accuracy | Are the health-related claims factually correct? | |
| Relevance | Does the answer address both benefits and risks? | |
| Completeness | Does it include important qualifications or limitations? | |
| Source Quality | Are the cited sources reliable for health information? | |
| Citation Quality | Do the sources support the specific claims? | |
| Overall Assessment | What is the strongest point and the main weakness? | |

**Case Study Question:** Based on your findings, would you consider this AI Overview reliable? Explain your answer using evidence from the claims and sources you checked.

## 6. Knowledge Check

### 1. What does accuracy measure?

- A. Whether the answer is visually attractive
- B. Whether the information is factually correct
- C. Whether the answer is short
- D. How many citations appear

### 2. An answer contains correct facts but does not address the user’s question. Which criterion is weak?

- A. Relevance
- B. Accuracy
- C. Source Quality
- D. Citation Quality

### 3. What does completeness measure?

- A. Whether every sentence has a citation
- B. Whether the answer includes essential information
- C. Whether the answer is written confidently
- D. Whether the answer contains technical terms

### 4. Why should evaluators check citations?

- A. To make answers longer
- B. To ensure sources support the claims
- C. To avoid reading the answer
- D. To count the number of websites

### 5. Ten claims are checked, and eight are factually correct. What is the Observed Accuracy Rate?

- A. 20%
- B. 70%
- C. 80%
- D. 100%

### 6. Can one metric fully measure an AI Overview’s quality?

- A. Yes, accuracy alone is enough
- B. Yes, if the answer has many citations
- C. No, different criteria measure different aspects of quality
- D. No, AI Overviews cannot be evaluated

### Answer Key

1. B
2. A
3. B
4. B
5. C
6. C

## 7. Recap

Evaluating Google AI Overviews requires checking more than whether an answer sounds convincing. Accuracy, relevance, completeness, source quality, and citation quality each reveal a different aspect of answer quality.

Evaluators can combine claim verification, source checking, and simple metrics to identify strengths and weaknesses. Ultimately, a reliable AI Overview should provide correct, relevant, sufficiently complete information supported by appropriate evidence.

## 8. References

1. Kakimov, R., Tan, X., Gillham, J., & Bejtic, N. (2026). *Auditing citation behavior in AI-generated search summaries: A framework and a case study of Google AI Overviews.* Proceedings of Machine Learning Research, 318, 224–235. https://proceedings.mlr.press/v318/kakimov26a.html
2. Xu, H., Iqbal, U., & Montgomery, J. M. (2026). *Measuring Google AI Overviews: Activation, source quality, claim fidelity, and publisher impact.* arXiv. https://doi.org/10.48550/arXiv.2605.14021

# Chapter 9: Limitations and Failure Modes — When AI Gets It Wrong

## Learning Objectives

By the end of this chapter, learners will be able to:

1. **Understand AI limitations:** Explain why Google AI Overviews can sometimes provide incorrect, incomplete, or misleading information.
2. **Identify common failure modes:** Describe common problems such as misunderstanding queries, using misleading information, losing context, and presenting outdated information.
3. **Understand contributing factors:** Explain how information gaps, ambiguous questions, and weaknesses in available sources can contribute to errors.
4. **Recognize potential risks:** Explain why incorrect AI-generated information can be harmful, particularly in health, safety, and other important decisions.
5. **Respond appropriately to errors:** Describe practical steps users can take when an AI Overview appears incorrect or unreliable.

## Introduction: When AI Gets It Wrong

Google AI Overviews help users understand topics quickly by summarizing information from web sources. However, these summaries are not always correct. An AI Overview may misunderstand a question, present information without important context, or provide an answer that is not adequately supported by available evidence.

Google acknowledges that AI Overviews can make mistakes. In its May 2024 explanation of early errors, Google identified problems involving misunderstood queries, misleading content, and limited high-quality information. These examples demonstrate that AI-generated summaries can fail for several different reasons.

Understanding these limitations is important because a confident, well-written answer may still be incorrect or misleading. Users should recognize common failure modes and know when to investigate further rather than automatically trusting the summary.

This chapter explores common ways Google AI Overviews can get information wrong, why these failures occur, and how users can respond responsibly.

## Key Terms

### 1. Failure Mode

A recurring way in which a system produces an incorrect, incomplete, or otherwise undesirable result.

**Simple explanation:** A failure mode is a common way that AI can go wrong.

### 2. Hallucination

In generative AI, a hallucination occurs when a system produces information that is false, fabricated, or unsupported by available evidence.

**Simple explanation:** A hallucination happens when AI gives information that sounds believable but is not adequately grounded in facts.

### 3. Ambiguous Query

A question or search request that has more than one possible interpretation.

**Simple explanation:** An ambiguous query is a question that AI may understand in the wrong way.

### 4. Information Gap

A situation in which reliable, relevant information about a topic is limited or unavailable.

**Simple explanation:** An information gap occurs when there is not enough good information available to answer a question reliably.

### 5. Context Loss

The omission or misunderstanding of important details, conditions, or qualifications that change the meaning of information.

**Simple explanation:** Context loss happens when AI leaves out details needed to understand an answer correctly.

### 6. Outdated Information

Information that was once accurate but is no longer current or applicable.

**Simple explanation:** Outdated information is information that may no longer be correct because circumstances have changed.

### 7. Overgeneralization

Applying a finding, rule, or conclusion too broadly when it may only be valid under particular conditions.

**Simple explanation:** Overgeneralization happens when AI makes a statement sound true for everyone or every situation, even when exceptions exist.

### 8. Overreliance on AI

Depending too heavily on AI-generated information without independently checking important claims.

**Simple explanation:** Overreliance means trusting AI too much without checking whether its answer is correct.

## Main Explanation

### 9.1 Misunderstanding the User’s Question

One possible failure mode occurs when an AI Overview interprets a search query differently from what the user intended.

Search queries are often short, informal, or ambiguous. A word may have several meanings, or a question may lack details needed to determine the user’s actual needs. As a result, the generated summary may answer a different question from the one the user intended to ask.

**Example:**

A user searches:

> “What is the best treatment for a cold?”

The user may be asking about the common cold, but the word “cold” can have other meanings in different contexts. If the system misinterprets the request, the resulting answer may be irrelevant to the user’s needs.

**Why This Matters:**

An answer can be logically written but still be unhelpful if it responds to the wrong question. Users should make their questions specific and check whether the response matches their intended meaning.

### 9.2 Hallucinations and Unsupported Information

Generative AI systems can produce statements that sound convincing but are false or not adequately supported by evidence. This is commonly described as hallucination.

In Google AI Overviews, errors can also arise when the system draws on misleading web content or interprets information incorrectly. Google has publicly acknowledged examples of inaccurate and unhelpful AI Overviews, including cases involving misleading content and misunderstood language.

**Example:**

A user asks whether a particular food cures a disease. An AI Overview might present a claim suggesting that the food has a proven medical benefit, even though the available evidence does not establish that conclusion.

The claim may sound scientific, but its wording could exaggerate what the evidence actually shows.

**Why This Matters:**

A convincing explanation is not proof that a claim is true. Users should verify important statements against reliable sources, particularly when health or safety is involved.

### 9.3 Information Gaps and Misleading Sources

AI Overviews depend on information available through the web. When reliable information about a question is limited, the system may encounter material that is satirical, irrelevant, misleading, or unsuitable for answering the question.

Google described this problem in its May 2024 explanation of AI Overview errors. One example involved the question “How many rocks should I eat?” There was little serious information addressing the question, while satirical content was available online. This illustrated how an information gap combined with misleading content could contribute to an inappropriate answer.

**Example:**

A user asks for a scientifically supported way to improve memory. Search results contain several credible educational resources but also a website making exaggerated claims about an unproven supplement.

If misleading content is selected or interpreted incorrectly, an AI Overview could give the impression that the supplement’s benefits are scientifically established.

**Why This Matters:**

The presence of information on the internet does not guarantee that it is reliable. When high-quality evidence is limited, users should be especially cautious about strong or unusual claims.

### 9.4 Context Loss and Overgeneralization

An AI Overview may summarize information so briefly that important conditions, exceptions, or qualifications are lost.

A research finding may apply only to a particular population, a specific situation, or a limited set of circumstances. If an answer removes those qualifications, the result may give readers a misleading impression.

**Example:**

A study finds that a particular exercise program improves one health outcome among a group of adults under specific conditions.

An AI Overview summarizes the finding as:

> “This exercise program improves everyone’s health.”

The summary makes a broader claim than the original evidence supports.

**Why This Matters:**

A simplified answer is not necessarily a faithful representation of the original information. Users should check whether the answer preserves important conditions and whether its conclusions are broader than the available evidence justifies.

### 9.5 Outdated or Conflicting Information

Information available online can change over time. Medical recommendations, government policies, product details, prices, and other time-sensitive facts may become outdated.

Sources can also disagree because they were published at different times, use different methods, or address different circumstances. A short AI-generated summary may not clearly explain these differences.

**Example:**

A user asks about current visa requirements. One webpage describes an earlier policy, while an official government website provides updated requirements.

If the older information is used without recognizing the change, the answer may mislead the user.

**Why This Matters:**

The age and context of information matter. For time-sensitive questions, users should check current official sources rather than relying exclusively on a summary.

### 9.6 False Confidence and Overreliance

AI Overviews present information in a concise, organized format. This can make an answer appear authoritative, even when some claims are uncertain or incorrect.

The problem is not only that an AI Overview may contain an error. It is also that users may accept the answer without checking it.

**Example:**

A student uses an AI Overview to answer an assignment question. Because the response is clearly written and includes links, the student copies it without opening the sources. The answer contains an incorrect interpretation of the topic, which the student then repeats in the assignment.

**Why This Matters:**

Clear writing and linked sources do not guarantee correctness. Users should treat AI Overviews as a starting point for understanding a topic, not as unquestionable authority.

### 9.7 High-Stakes Errors: When Mistakes Can Cause Harm

Some incorrect answers are more consequential than others. A mistake about a minor fact may cause little harm, while an error involving medical treatment, legal obligations, financial decisions, or physical safety may have serious consequences.

For these topics, users need to consider both the possibility of error and the consequences of acting on incorrect information.

**Example:**

A user searches for advice about mixing two medications. An AI Overview provides a general statement that the combination is safe but does not account for the user’s dosage, medical history, or other medications.

Relying on that summary alone could be dangerous.

**Why This Matters:**

AI-generated summaries cannot replace individualized professional advice when a decision requires it. Users should consult qualified professionals or appropriate official sources for important health, legal, financial, or safety-related decisions.

### 9.8 How Should Users Respond When AI Gets It Wrong?

Recognizing a possible failure is only the first step. Users should also know how to respond.

1. **Identify the questionable claim.** Find the specific statement that appears incorrect, misleading, or incomplete.
2. **Open the cited sources.** Check whether the linked pages actually contain relevant information supporting the statement.
3. **Compare additional reliable sources.** Look for independent confirmation, giving preference to authoritative and current sources appropriate to the topic.
4. **Check the context and date.** Determine whether the information is current and whether important conditions or exceptions have been omitted.
5. **Avoid acting on uncertain high-stakes advice.** If an answer concerns health, safety, legal obligations, or significant financial decisions, consult an appropriate professional or official source before acting.
6. **Provide feedback when appropriate.** Google encourages users to report AI Overview responses that appear incorrect. Feedback can help Google identify and investigate problems.

**Key Takeaway:** Users cannot eliminate every AI error, but they can reduce the risk of being misled by checking evidence, considering context, and responding cautiously to uncertain information.

## Practical Case Study: When an AI Overview Misinterprets a Question

**Research Question:** How can an AI Overview produce a misleading answer when reliable information is limited?

### Background

In May 2024, Google discussed an unusual AI Overview error involving the question “How many rocks should I eat?” Google explained that the web contained little serious information answering this question, while satirical content was available. This case illustrated how limited reliable information and misleading content could contribute to an inappropriate response.

**Objective:** To understand how information gaps and misleading sources can contribute to AI Overview failures.

### Case Analysis

| Evaluation Point | Case Study Finding |
|---|---|
| **User Query** | “How many rocks should I eat?” |
| **Main Problem** | The question had little relevant, serious information available online. |
| **Contributing Factor** | Satirical content was among the available material. |
| **Failure Mode** | The answer did not appropriately handle the unusual query and limited reliable evidence. |
| **Potential Risk** | A user could mistake an inappropriate answer for genuine advice. |
| **Lesson** | When a query is unusual and reliable evidence is limited, an AI system should avoid presenting misleading advice as a trustworthy answer. |

### Why This Matters

This real example shows that an AI Overview can go wrong even when information exists on the web. The available material may not be suitable for answering the question, and the system may fail to recognize that limitation.

### Conclusion

The case demonstrates the importance of recognizing information gaps, distinguishing serious evidence from satire, and treating unusual or potentially dangerous answers with caution. It also shows why AI systems should sometimes avoid providing a confident answer when the available information is unsuitable.

**Source:** Google, “AI Overviews: About last week” (May 30, 2024).

## Fun Fact

After unusual AI Overview results attracted attention in May 2024, Google described several changes intended to reduce similar problems. These included better detection of nonsensical queries, limits on the use of some user-generated content that could provide misleading advice, and changes to when AI Overviews appear.

This illustrates an important point: identifying recurring failure patterns can help developers improve AI systems.

## Knowledge Check

### Question 1. What is a failure mode?

- A. A method for making AI responses longer.
- B. A recurring way in which a system produces an incorrect or undesirable result.
- C. A type of search engine.
- D. A method for ranking websites.

### Question 2. What is an AI hallucination?

- A. When AI provides information that is false or unsupported by available evidence.
- B. When AI displays too many links.
- C. When a user asks a question twice.
- D. When an AI Overview is short.

### Question 3. Why can information gaps contribute to AI Overview errors?

- A. They guarantee that every available source is false.
- B. They prevent users from searching the web.
- C. They may leave the system with limited reliable information and unsuitable material.
- D. They automatically make an answer outdated.

### Question 4. An AI Overview describes a finding from a small study as true for everyone. Which failure mode does this illustrate?

- A. Context loss or overgeneralization.
- B. Improved relevance.
- C. Better source selection.
- D. Accurate summarization.

### Question 5. A user asks about current visa requirements, but an AI Overview relies on an old webpage. What is the main concern?

- A. The answer is necessarily irrelevant.
- B. The information may be outdated.
- C. The query is necessarily ambiguous.
- D. The answer is too concise.

### Question 6. What should a user do before relying on AI-generated medical advice?

- A. Trust it if the answer sounds confident.
- B. Read only the first sentence.
- C. Verify the information using appropriate reliable sources and consult a qualified professional when needed.
- D. Assume the linked sources guarantee correctness.

## Answer Key

1. B
2. A
3. C
4. A
5. B
6. C

## Recap

Google AI Overviews can help users understand information quickly, but they have limitations that users should recognize.

Common failure modes include:

- **Misunderstanding queries:** Answering a question differently from what the user intended.
- **Hallucinations and unsupported information:** Presenting false or insufficiently supported claims.
- **Information gaps and misleading sources:** Drawing on material that is limited, satirical, or unsuitable for the question.
- **Context loss and overgeneralization:** Omitting qualifications or applying findings too broadly.
- **Outdated or conflicting information:** Failing to reflect current information or explain differences between sources.
- **False confidence and overreliance:** Encouraging users to accept a clear-sounding answer without verification.
- **High-stakes errors:** Providing information that could lead to harmful decisions if followed without further checking.

These failures can arise for different reasons, and not every AI Overview will exhibit them. Understanding the possible causes helps users recognize warning signs and respond appropriately.

Ultimately, AI Overviews should be treated as a starting point for research rather than an unquestionable authority. Checking reliable sources, considering context, and seeking professional guidance when necessary can reduce the risk of being misled.

## References

1. Google. (2024, May 30). *AI Overviews: About last week.*
2. Google Search Help. *Find information in faster & easier ways with AI Overviews in Google Search.*
3. Google People + AI Research (PAIR). *Errors + Graceful Failure.*

# Topic 12: The Business Side
How AI search changes money, traffic and power
## 12.1 Zero-click search and traffic loss

**In simple terms:** You ask a librarian a question and she just tells you the answer, so you never open the book. Google’s AI now answers on the page, so people don’t click through. The sites that wrote the information lose visitors.

**What it is:** Zero-click search is when users get what they need from a search engine or AI without clicking any website.

**Why it matters:** AI makes finding information easier for users but harder for businesses that depend on website traffic.

**Business impact:** Fewer visitors can mean less advertising income and fewer sales.

**Example:** A user asks Google’s AI Overview for the best laptops and reads the answer without visiting a single review site.

### Research Findings

- SparkToro found 68% of US Google searches ended with no click in early 2026, up from 60.45% in 2024.
- A randomised experiment found AI Overviews cut outbound organic clicks by 39.8% and raised zero-click searches by 34.5%.
- Pew measured an 8% click rate with an AI Overview versus 15% without. Google disputes Pew’s methodology.
- Seer Interactive found informational-query click-through fell from 1.76% to 0.61% between June 2024 and September 2025, yet brands cited inside the overview got 35% more organic clicks than uncited ones.
- The damage is uneven: health content was hit hardest (34% click decline), while local services lost only 5%.
- Gartner forecasts organic search traffic will fall by 50% or more by 2028. That is a prediction, not a measurement.

### Sources

Search Engine Land on SparkToro: [https://searchengineland.com/google-zero-click-searches-2026-study-479717](https://searchengineland.com/google-zero-click-searches-2026-study-479717)
PPC Land on the field experiment: [https://ppc.land/all-about-berlin-loses-75-of-traffic-as-zero-click-searches-hit-68/](https://ppc.land/all-about-berlin-loses-75-of-traffic-as-zero-click-searches-hit-68/)
SoftwareSeni (Pew figures): [https://www.softwareseni.com/60-zero-click-the-numbers-that-rewrite-every-traffic-assumption/](https://www.softwareseni.com/60-zero-click-the-numbers-that-rewrite-every-traffic-assumption/)
Beancount (Google disputes Pew): [https://beancount.io/blog/2026/08/14/ai-overviews-zero-click-search-small-business-guide](https://beancount.io/blog/2026/08/14/ai-overviews-zero-click-search-small-business-guide)
Bosio Digital (Seer data): [https://bosio.digital/articles/ai-overviews-zero-click-search](https://bosio.digital/articles/ai-overviews-zero-click-search)
Searchlab: [https://searchlab.nl/en/statistics/zero-click-searches-statistics-2026](https://searchlab.nl/en/statistics/zero-click-searches-statistics-2026)
LLMrefs (Gartner): [https://llmrefs.com/blog/zero-click-search](https://llmrefs.com/blog/zero-click-search)
## 12.2 From SEO to GEO

**In simple terms:** SEO is getting your lemonade stand to the front of the street. GEO is getting the AI to say “go buy lemonade from that stand.” The old goal was to be first in the list. The new goal is to be the one the AI mentions.

**What it is:** SEO (Search Engine Optimization) helps sites rank in traditional results. GEO (Generative Engine Optimization) makes content more likely to be included in AI-generated answers.

**Why it matters:** Visibility now depends on being cited, not just ranked.

**Business impact:** Companies must change their online marketing to stay visible.

**Example:** A company organises its site with clear explanations, reliable sources and useful facts so AI systems can understand and reference it.

### Research Findings

- GEO began with a Princeton, Georgia Tech, IIT Delhi and Allen Institute paper, presented at ACM SIGKDD 2024, that built a 10,000-query benchmark and tested nine strategies.
- The best tactics were adding statistics, quotes and cited sources, with gains of up to 40%. Keyword stuffing produced near-zero or negative results.
- A vendor summary says position-5 pages gained +115% visibility while position-1 pages gained almost nothing.
- Studies disagree on what AI cites. Yext found 86% of AI answers rely on brand-managed content, while Fullintel/UConn found 47% of citations came from journalistic sources and over 89% of cited links were earned media.
- Unverified vendor claims: 65% of AI bot hits target content less than a year old.

### Sources

LLM Pulse, GEO guide: [https://llmpulse.ai/blog/geo-guide/](https://llmpulse.ai/blog/geo-guide/)
Paz, GEO glossary: [https://www.paz.ai/glossary/generative-engine-optimization-geo](https://www.paz.ai/glossary/generative-engine-optimization-geo)
Sonar, GEO tools: [https://trysonar.app/blog/generative-engine-optimization-tools](https://trysonar.app/blog/generative-engine-optimization-tools)
Averi: [https://www.averi.ai/learn/the-definitive-guide-to-geo-get-cited-by-ai-in-2026](https://www.averi.ai/learn/the-definitive-guide-to-geo-get-cited-by-ai-in-2026)
eMarketer (Yext): [https://www.emarketer.com/topics/category/perplexity/3](https://www.emarketer.com/topics/category/perplexity/3)
Systems Architect (Fullintel/UConn): [https://systemsarchitect.net/?p=159](https://systemsarchitect.net/?p=159)
RankAI: [https://rankai.ai/articles/how-to-do-geo](https://rankai.ai/articles/how-to-do-geo)
Aggarwal et al., “GEO: Generative Engine Optimization” (KDD 2024, original paper)
## 12.3 AI-referred traffic quality

**In simple terms:** Not many people visit a site because an AI sent them. Those who do are usually keen, like a friend saying “you’ll love this.” They stay longer and are likelier to buy.

**What it is:** AI-referred traffic is visitors who arrive through links in AI tools.

**Why it matters:** These visitors may behave differently from traditional search visitors.

**Business impact:** Businesses should measure not just how many visitors AI brings but whether they stay, buy or become customers.

**Example:** Someone asks an AI to compare phones, clicks a recommended product link, and arrives ready to buy.

### Research Findings

- Volume is tiny: SE Ranking puts AI at 0.32% of web traffic, while Conductor’s larger sample says about 1.08%.
- Conversion is higher, but the gap depends on the study: between 1.2x and 9x better than Google organic. One B2B study found 14.2% versus 2.8%.
- It isn’t universal: one cohort found the pattern reverses for e-commerce, with organic at 2.1% against AI at 1.6%. Small samples can also skew the percentages.

### Sources

Mean CEO: [https://blog.mean.ceo/?p=11356](https://blog.mean.ceo/?p=11356) and [https://blog.mean.ceo/?p=11360](https://blog.mean.ceo/?p=11360)
Analyze (Conductor): [https://www.tryanalyze.ai/blog/ai-traffic-study](https://www.tryanalyze.ai/blog/ai-traffic-study)
Product Hunt roundup (Opollo): [https://www.producthunt.com/p/rankfender/the-10-highest-converting-channels-in-2026](https://www.producthunt.com/p/rankfender/the-10-highest-converting-channels-in-2026)
Alian Software: [https://aliansoftware.com/en/blog/18-months-of-ai-search-data-smb-traffic-conversions](https://aliansoftware.com/en/blog/18-months-of-ai-search-data-smb-traffic-conversions)
AirOps: [https://airops.com/blog/ai-referral-traffic-conversion-rates](https://airops.com/blog/ai-referral-traffic-conversion-rates)
## 12.4 Ads inside AI answers

**In simple terms:** Companies pay to have products shown next to the AI’s answer, like a billboard beside a road sign. Some AI companies do it and some refuse, because people may stop trusting answers they think were paid for.

**What it is:** AI companies can earn money by showing ads or sponsored recommendations inside or beside AI answers.

**Why it matters:** It opens new advertising revenue but may make users doubt whether recommendations are neutral.

**Business impact:** A new ad channel for brands, with transparency and trust as the key risks.

**Example:** Asked for running shoes, an assistant shows a clearly labelled sponsored product alongside other picks.

### Research Findings

- ChatGPT turned on ads on February 9, 2026, for Free and Go users only, with a $50,000 minimum and a $60 CPM. It passed $100 million in annualized revenue within six weeks of launch.
ChatGPT Ad Formats vs Other AI Assistants: A 2026 Buyer's Map
- Google shows ads inside AI Overviews and AI Mode but not the standalone Gemini app (as of April 2026), in about 25.5% of AI Mode responses.
- Perplexity abandoned advertising in February 2026 and went subscription-only. Claude has publicly committed to staying ad-free.
- One estimate says about 80% of 2026 AI ad spending will appear beside AI content rather than inside chatbots.
- Under “answer independence,” platforms say ad revenue does not influence the substance of the AI’s answers. That is a company promise users can’t check.

### Sources

Thrad: [https://www.thrad.ai/content/advertising-on-chatgpt-vs-perplexity-vs-claude-vs-gemini](https://www.thrad.ai/content/advertising-on-chatgpt-vs-perplexity-vs-claude-vs-gemini)
Thrad, ad formats: [https://www.thrad.ai/content/chatgpt-ad-formats-vs-other-ai-assistants](https://www.thrad.ai/content/chatgpt-ad-formats-vs-other-ai-assistants)
Thrad mirror (revenue figure): [https://neugenm.thrad.ai/content/chatgpt-ad-formats-vs-other-ai-assistants](https://neugenm.thrad.ai/content/chatgpt-ad-formats-vs-other-ai-assistants)
GrowthSpree: [https://www.growthspreeofficial.com/blogs/advertising-on-ai-platforms-b2b-saas-2026](https://www.growthspreeofficial.com/blogs/advertising-on-ai-platforms-b2b-saas-2026)
eMarketer: [https://www.emarketer.com/content/perplexity-retreat-ads-marks-split-on-ai-monetization-models](https://www.emarketer.com/content/perplexity-retreat-ads-marks-split-on-ai-monetization-models)
Adventure PPC: [https://www.adventureppc.com/blog/chatgpt-ads-vs-perplexity-ads-2026-ai-search-advertising-comparison](https://www.adventureppc.com/blog/chatgpt-ads-vs-perplexity-ads-2026-ai-search-advertising-comparison)
## 12.5 Publisher licensing and revenue sharing

**In simple terms:** News sites write the stories AI learns from. Licensing deals mean the AI company pays for the right to use them. Some pay once, and some share the money the AI earns each time a story helps answer a question.

**What it is:** AI systems use news, books and other publications. Licensing lets AI companies pay for permission to use certain content.

**Why it matters:** Publishers may earn licensing money but lose advertising revenue if readers stop visiting.

**Business impact:** Publishers and AI companies are negotiating how content is used and how creators are paid.

**Example:** An AI company agrees to use a news organisation’s articles in its answers.

### Research Findings

- Two models: OpenAI pays a flat licensing fee, while Perplexity offers a “double-digit” revenue cut. OpenAI’s media-partnerships VP was asked about revenue sharing in June 2026 and answered “Not at this point”.
- Marketplaces: Perplexity set aside a $42.5 million pool. Microsoft launched its Publisher Content Marketplace in February 2026 as a pay-per-use platform where publishers set their own terms. Amazon’s wider marketplace was still exploratory as of July 2026.
- Deal sizes: OpenAI has deals with about 35 publishers and Perplexity about 20. Reported amounts: Thomson Reuters $33 million in AI licensing revenue, People Inc. at least $16 million a year from OpenAI, and the New York Times about $20 million a year from Amazon. Wiley reported $44M+ across several AI contracts. Counts conflict: Tow Center tracking found 13 partners for one big-tech program while Amazon says it has over 200 deals.
- Who gets in: Independent publishers are not yet eligible for many direct deals.
- Anthropic: it has done few licensing deals and instead agreed to a proposed $1.5 billion copyright settlement, which at that source’s August update still needed final approval.
- Crawler economics: Cloudflare’s 2025 crawl-to-referral ratios were Google 14:1, OpenAI 1,700:1, Anthropic 73,000:1, and its July 2026 dashboard showed 118 to nearly 50,000 crawls per referral. Figures differ between releases, so cite the date. One sports site reportedly got 13 million AI-bot visits a month but only 600 human users.
- Pay Per Crawl: launched in private beta on July 1, 2025, letting publishers allow, charge for, or block each crawler. Cloudflare said it would block mixed-use crawlers from ad-supported pages by default starting September 15, 2026, while search crawlers still get in. I haven’t confirmed how the rollout went. It is also moving toward paying publishers only when their content shows up in a generated answer.
- Blocking has a cost: Rutgers and Wharton research attributed the traffic lost from blocking mainly to reduced brand exposure inside AI answers rather than forgone referral clicks.

### Sources

eMarketer, deals: [https://www.emarketer.com/content/openai--perplexity-secure-more-publisher-licensing-deals](https://www.emarketer.com/content/openai--perplexity-secure-more-publisher-licensing-deals)
Studio Global (OpenAI stance): [https://studioglobal.ai/discover/answers/what-is-openai-s-stance-on-sharing-ad-6a202e502354ec6e1b5f1991](https://studioglobal.ai/discover/answers/what-is-openai-s-stance-on-sharing-ad-6a202e502354ec6e1b5f1991)
LLM Pulse: [https://llmpulse.ai/blog/ai-content-deals-beyond-openai/](https://llmpulse.ai/blog/ai-content-deals-beyond-openai/) and [https://llmpulse.ai/blog/ai-content-licensing-deals/](https://llmpulse.ai/blog/ai-content-licensing-deals/)
Digital Content Next: [https://digitalcontentnext.org/blog/category/research/page/2/](https://digitalcontentnext.org/blog/category/research/page/2/)
Pebblous: [https://blog.pebblous.ai/blog/ai-content-licensing-market-leverage/en/](https://blog.pebblous.ai/blog/ai-content-licensing-market-leverage/en/)
Digiday: [https://digiday.com/media/publishers-scorecard-for-big-techs-ai-licensing-deals/](https://digiday.com/media/publishers-scorecard-for-big-techs-ai-licensing-deals/)
New or Media: [https://newormedia.com/blog/?p=1500](https://newormedia.com/blog/?p=1500)
Let’s Data Science (Cloudflare): [https://letsdatascience.com/news/cloudflare-gives-publishers-control-over-ai-crawlers-3f1384fa](https://letsdatascience.com/news/cloudflare-gives-publishers-control-over-ai-crawlers-3f1384fa)
Startup Fortune: [https://startupfortune.com/?p=15343](https://startupfortune.com/?p=15343)
PPC Land: [https://ppc.land/cloudflare-stops-charging-ai-per-crawl-and-starts-paying-per-answer/](https://ppc.land/cloudflare-stops-charging-ai-per-crawl-and-starts-paying-per-answer/) and [https://ppc.land/crawl-to-referral-ratio/](https://ppc.land/crawl-to-referral-ratio/)
Tech Policy Press: [https://techpolicy.press/cloudflare-wades-into-the-battle-over-ai-consent-and-compensation](https://techpolicy.press/cloudflare-wades-into-the-battle-over-ai-consent-and-compensation)
## 12.6 Market share and platform competition

**In simple terms:** This is who’s winning the race. Google is still the giant, ChatGPT is the biggest AI chatbot, and others like Gemini are catching up, like several ice cream shops fighting over one neighbourhood.

**What it is:** Market share is the portion of a market a company controls. AI search has increased competition for users.

**Why it matters:** Companies compete on answer quality, speed, accuracy, integration with other services and access to information.

**Business impact:** The companies users prefer gain customers, data and revenue opportunities.

**Example:** Google builds AI into its search engine, while OpenAI offers ChatGPT with web search.

### Research Findings

- Google still holds roughly 90% of global search, though its US share slipped from 87.28% to 84.17% year over year.
- ChatGPT had 900 million weekly active users in January 2026. In March, Gemini overtook Perplexity as the second-largest AI referral source.
- Estimates of ChatGPT’s share of AI search conflict: 42.3% in one report and 73.62% of US chatbot share in another. They measure different things (queries, referrals, users), so always state the metric.

### Sources

WebFX: [https://www.webfx.com/data/google-vs-bing/](https://www.webfx.com/data/google-vs-bing/)
Alice Labs: [https://alicelabs.ai/en/insights/ai-search-users-2026](https://alicelabs.ai/en/insights/ai-search-users-2026)
Mean CEO: [https://blog.mean.ceo/?p=4572](https://blog.mean.ceo/?p=4572)
Texta: [https://texta.ai/blog/ai-search-market-share-2026-complete-analysis](https://texta.ai/blog/ai-search-market-share-2026-complete-analysis)
## 12.7 Legal and power dynamics

**In simple terms:** Some companies say the AI used their work without asking, so they sue. It’s like one kid saying “you copied my homework” and a judge deciding who’s right.

**What it is:** AI raises legal and business questions about copyright, data ownership, competition and who controls access to information.

**Why it matters:** Court outcomes and new rules affect how AI companies collect data, use published content and compete.

**Business impact:** The results could decide how revenue is shared and how much control publishers keep.

**Example:** A news publisher argues an AI company used its articles without permission or payment.

### Research Findings

- The NYT sued OpenAI in December 2023. In January 2026 the judge upheld an order for OpenAI to produce 20 million chat logs.
- Mid-2025 rulings in Bartz v. Anthropic and Kadrey v. Meta found AI training can be fair use, but they don’t bind the Times case.
- The NYT sued Perplexity in December 2025, and Dow Jones had sued it in October 2024. Claims are shifting from training toward the distribution layer, where AI turns reporting into answers.
- A Munich court ruled in November 2025 that OpenAI violated German copyright law.
- Case counts vary, from more than 40 to more than 70. In these sources I found no final ruling on the core fair-use question for AI search.

### Sources

Everything PR: [https://everything-pr.com/nyt-v-openai-30-months-times-answer-engine-blockade-publishers-2026](https://everything-pr.com/nyt-v-openai-30-months-times-answer-engine-blockade-publishers-2026)
Axios: [https://www.axios.com/2025/12/05/nyt-sues-perplexity-for-copyright-infringement](https://www.axios.com/2025/12/05/nyt-sues-perplexity-for-copyright-infringement)
TheWrap: [https://www.thewrap.com/?p=7905152](https://www.thewrap.com/?p=7905152)
Texxr: [https://texxr.com/893303](https://texxr.com/893303)
Generative AI lawsuit timeline: [https://sustainabletechpartner.com/topics/ai/generative-ai-lawsuit-ti](https://sustainabletechpartner.com/topics/ai/generative-ai-lawsuit-ti)
OODA Loop: [https://oodaloop.com/briefs/technology/new-york-times-sues-a-i-start-up-perplexity-over-use-of-copyrighted-work](https://oodaloop.com/briefs/technology/new-york-times-sues-a-i-start-up-perplexity-over-use-of-copyrighted-work)
Tech Policy Press: [https://techpolicy.press/cloudflare-wades-into-the-battle-over-ai-consent-and-compensation](https://techpolicy.press/cloudflare-wades-into-the-battle-over-ai-consent-and-compensation)
