<img width="2816" height="1536" alt="image" src="https://github.com/user-attachments/assets/5bfae9c4-9fea-472c-ac15-271479c0e1e3" /># Chapter 3. LLM Fundamentals

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

![A pipeline of the training stages an LLM passes through](https://wmpyxajsoiwnvxkmfqty.supabase.co/storage/v1/object/public/website_images/blog_post_images/Gemini_Generated_Image_s7kdtts7kdtts7kd.png)

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
