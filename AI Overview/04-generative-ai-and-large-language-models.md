# 04 Generative AI & Large Language Models

The models that write: what generative AI is, how large language models are built and how they produce text, what they can and can't do, and the tools people actually use.

---

## 4.1 What Generative AI Is

Generative AI creates new content (text, images, audio, video, code) that looks like the data it learned from.

Most earlier ML is **predictive** (or discriminative): it labels or scores existing data, like "spam / not spam" or a house price (Topic 3).

### Predictive vs generative AI

| | Predictive AI | Generative AI |
|---|---|---|
| **Output** | A label, number or decision | New text, images, audio, video or code |
| **Example** | Fraud score for a card payment | A written answer, an essay draft, a picture |
| **Typical models** | Logistic regression, random forests, CNN classifiers | LLMs (Transformers), diffusion models, GANs |

### How the ideas nest

**AI ⇒ machine learning ⇒ deep learning ⇒ generative AI ⇒ large language models (LLMs)**

A **large language model (LLM)** is a generative model for language: a very large Transformer network trained to predict the next token of text.

### Expanded context from Research Notes (Deep Learning section)

Deep learning is machine learning with artificial neural networks that have many layers. "Deep" just means many layers. Each layer learns a slightly more abstract version of the input: in an image, early layers spot edges, middle layers spot shapes, final layers spot faces or cars. Unlike classical ML, you don't have to hand-pick the features.

Generative AI is deep learning that creates new content. The Transformer architecture (from "Attention Is All You Need," 2017) is the basis of modern LLMs. It is a type of neural network that uses **self-attention** to process all tokens in parallel, which made training on huge datasets with GPUs practical.

---

## 4.2 Key LLM Vocabulary

| Term | What it means | Why it matters |
|------|---------------|----------------|
| **Token** | The unit an LLM reads and writes: a word or part of a word. A common rule of thumb is that 1 token ≈ ¾ of an English word, so 1,000 tokens ≈ 750 words. | Usage limits and prices are counted in tokens. |
| **Parameters** | The adjustable numbers (weights) inside the network, learned in training. GPT-3 (2020) had 175 billion. | More parameters can store more patterns, but cost more to train and run. |
| **Context window** | How many tokens the model can take in at once: your prompt, files, the conversation so far and its own reply. Leading models in 2026 handle around 1 million tokens. | It works like short-term memory. Anything outside the window is forgotten, and long inputs are not read equally well (Topic 9, "Lost in the Middle"). |
| **Training data** | The huge text collection (web pages, books, code) used in pretraining. | The model's knowledge and its biases come from this data. |
| **Knowledge cutoff** | The date the training data ends. | Later events are unknown unless the model searches (Topic 9). |
| **Prompt** | The input instructions and content you give the model. | Clear prompts give better answers (4.9). |
| **Inference** | Running a trained model to produce an answer. | Every answer has a computing cost, which is why AI answers cost more than a list of links (Topic 12). |

### Expanded context from Research Notes (NLP section)

**Tokenization** is the first step in NLP: splitting text into tokens (words or word pieces). "I loved it!" becomes I / loved / it / !. Modern LLMs use **subword tokenization** (like byte-pair encoding) to split rare words into common pieces, e.g. "unbelievably" → un / believe / ably. This lets the model handle new words, typos and names without needing every word in its vocabulary.

**Embeddings** turn words into numbers: each token becomes a vector called an embedding. Words used in similar ways get similar vectors, so "good" is closer to "great" than to "table." Modern models use **contextual embeddings** (from BERT/GPT), where the vector for a word changes with the sentence, so "bank" (river) and "bank" (money) get different vectors.

---

## 4.3 How an LLM Is Built

### Step 1 — Pretraining (self-supervised learning)

The model reads a huge amount of text and repeatedly guesses the next token, then checks against the real next token. Nobody labels the data: the text itself provides the answers, which is why it is called **self-supervised**.

Training uses the same loop as Topic 3: predict → measure loss → backpropagation → gradient descent, repeated over trillions of tokens on thousands of GPUs.

The result is a **base model**: it can continue text fluently but doesn't reliably follow instructions or behave helpfully.

### Step 2 — The Transformer architecture ("Attention Is All You Need," Google, 2017)

- **Self-attention:** for each token, the model scores how relevant every other token is and blends in their information. In "The animal didn't cross the street because it was too tired," attention helps link "it" to "animal."
- **Parallel processing:** unlike older RNNs, which read one word at a time, Transformers process all tokens at once. That made training on huge datasets with GPUs practical.
- **Positional information** is added so the model knows word order.
- Many stacked layers of attention, each building a richer picture of meaning (like the edges → shapes → faces idea in Topic 3).

### Step 3 — Post-training (alignment)

Turns the base model into a helpful assistant. OpenAI's InstructGPT paper (2022) set out the standard three stages:

1. **Supervised fine-tuning (SFT) / instruction tuning:** human writers create good example answers to prompts, and the model is trained to imitate them.
2. **Reward model:** the model writes several answers to each prompt, humans rank them, and a separate reward model learns to predict which answers people prefer.
3. **Reinforcement learning (PPO):** the model is tuned to get high scores from the reward model, with a penalty that stops it drifting too far from the SFT model.

### Why alignment matters

In the InstructGPT study, people preferred answers from the aligned **1.3-billion-parameter** model over the original **175-billion-parameter** GPT-3. Training a model to be helpful mattered more than making it 100× bigger.

Steps 2 and 3 of this recipe are **RLHF** (reinforcement learning from human feedback). Labs also use variations, such as AI feedback guided by a written list of principles.

**The side effect to remember:** because people tend to rate agreeable answers highly, RLHF can teach **sycophancy** (Topic 9).

### Step 4 — Grounding and tools

At answer time, the model can be given retrieved web pages or documents (**RAG**, Topic 7) and tools such as search, a calculator or code. This adds fresh facts and lets it cite sources instead of relying only on memory.

### Expanded context from Research Notes (AI Search section)

**Retrieval-Augmented Generation (RAG)** was introduced in research by Lewis et al. (2020): a model first retrieves relevant documents and then generates an answer from them. An LLM alone only knows its training data (which has a cutoff date) and may invent facts. RAG gives it fresh, specific evidence and makes citations possible. Simple analogy: a closed-book exam (plain LLM) vs. an open-book exam (RAG).

**Grounding** means instructing and training the model to base its answer only on the retrieved sources and attach citations to specific claims. It reduces hallucination and lets users check the answer.

---

## 4.4 How an LLM Writes an Answer

### The process

1. Your prompt is split into **tokens** and turned into **embeddings** (Topic 5).
2. The Transformer layers process all the tokens and produce a probability for every possible next token.
3. One token is chosen, added to the text, and the process repeats, one token at a time, until the answer ends. This is called **autoregressive generation**.

### Temperature

Controls randomness:

| Temperature | Behavior |
|-------------|----------|
| **Low** | Picks the most likely tokens (focused, repeatable) |
| **High** | Picks less likely ones more often (varied, creative, more errors) |

That's why the same question can get different answers.

### Key consequence

The model picks text that is **likely**, not text that is **checked as true**. A plausible but wrong token sequence looks just as fluent as a correct one, which is the root of **hallucination** (Topic 8).

### Expanded context from Research Notes (Accuracy section)

OpenAI's 2025 paper "Why Language Models Hallucinate" gives two reasons:

1. **Pretraining:** models learn by predicting the next word from huge amounts of text that has no "true/false" labels. Regular patterns like spelling are learned reliably, but rare, arbitrary facts (like someone's birthday) can't be predicted from patterns, so the model guesses something plausible.
2. **Evaluation rewards guessing:** most benchmarks score only accuracy. Like a student on a multiple-choice test with no penalty for wrong answers, a model that guesses scores higher than one that says "I don't know." So training pushes models toward confident guessing.

The paper's example: on one test, a model that abstained 52% of the time had a 26% error rate, while an older model that almost always answered had slightly higher accuracy but a 75% error rate. The suggested fix is to penalize confident errors more than honest uncertainty.

---

## 4.5 Reasoning Models

### What they are

Newer "reasoning" or "thinking" models generate a hidden chain of intermediate steps before the final answer (**chain-of-thought**), and spend more computing time per question (**test-time compute**). They are trained, often with reinforcement learning, to work through problems step by step.

### Strengths

- Math
- Coding
- Logic puzzles
- Multi-step planning

### Trade-offs

- Slower and more expensive per answer
- Still brittle: Apple's GSM-Symbolic study found reasoning models also dropped when irrelevant sentences were added (Topic 9)

### Expanded context from Research Notes (Limitations section)

Apple's GSM-Symbolic (2024) made templated versions of the GSM8K grade-school math benchmark across 25 models. Just changing names and numbers made scores drop and vary. Adding more steps made performance fall further. Adding one irrelevant sentence ("GSM-NoOp") caused drops of up to 65%. The researchers argue current models rely on probabilistic pattern matching rather than true logical reasoning. Newer reasoning models do better, but they still showed drops.

---

## 4.6 Beyond Text: Images, Audio and Video

### Multimodal models

Take in and produce several types of data: you can show a photo, chart or screenshot and ask about it, talk by voice, or ask for an image.

AI Mode queries using voice, images or documents are already **1 in 5** (Topic 1).

### Diffusion models

(Stable Diffusion, Midjourney, most video generators): in training, noise is gradually added to real images and the model learns to remove it step by step. To create an image, it starts from pure noise and "denoises" toward a picture that matches the text prompt.

### GANs (generative adversarial networks, 2014)

Two networks compete. A **generator** makes fakes and a **discriminator** tries to spot them; each improves the other. Used for early deepfakes and image tools, now largely replaced by diffusion for images.

### Expanded context from Research Notes (Deep Learning section)

**Diffusion models** and **GANs** are listed as main neural network architectures for generating images. Diffusion models are described as learning to remove noise step by step. GANs use a generator and discriminator trained against each other.

---

## 4.7 What Generative AI Can and Can't Do

| Strong at | Weak at / risky |
|-----------|-----------------|
| Writing, editing, rewriting in a different tone | Rare, specific facts (hallucination) |
| Summarizing and explaining | Recent events without search (knowledge cutoff) |
| Translating between languages | Exact arithmetic and counting without tools |
| Brainstorming ideas and options | Knowing when it is wrong (overconfidence) |
| Writing and explaining code | Staying neutral when the user pushes (sycophancy) |
| Answering questions in plain language | Very long inputs (lost in the middle); manipulation (prompt injection) |

### Summary

LLMs learn **patterns, not truth**. Regular patterns (grammar, style, common facts) are learned reliably; rare, arbitrary facts can't be predicted, so the model guesses something plausible.

### Expanded context from Research Notes (Limitations section)

**Knowledge limits:** A language model only "knows" what was in its training data, which ends at a fixed date called the knowledge cutoff. Anything after that (new laws, prices, sports results, who holds a job) is unknown to it unless it can search the web. The model also can't tell what it doesn't know: it may answer an "after cutoff" question with old information as if it were current.

**Sycophancy:** Sycophancy is when an AI tells users what they want to hear: agreeing with wrong claims, over-praising ideas, or changing a correct answer when the user pushes back. It happens because models are fine-tuned on human feedback (RLHF): people tend to rate agreeable, flattering answers higher, so the model learns that pleasing the user earns reward, even at the cost of honesty.

**Lost in the Middle:** Modern models can take in very long inputs, but they don't read all of it equally well. Stanford researchers (Liu et al., 2023) tested models on questions where the answer was hidden in one of many documents. Accuracy was highest when the key document was at the very beginning or end of the input, and dropped significantly when it was in the middle: a U-shaped curve. Performance also fell as the input got longer.

---

## 4.8 Who's Playing: The Tools People Actually Use

| Tool | Made by | Known for |
|------|---------|-----------|
| **ChatGPT** | OpenAI | Leading chatbot; 1B+ weekly users; search, voice, images; ads since 2026 |
| **Gemini** | Google | Powers AI Overviews and AI Mode; built into Android and Google apps |
| **Claude** | Anthropic | Chat assistant, used heavily for writing and coding |
| **Copilot** | Microsoft | Built into Windows and Office |
| **Perplexity** | Perplexity AI | Answer engine with numbered citations |
| **Grok** | xAI | Chatbot built into X; worst citation accuracy in the Tow test (Topic 7) |
| **DeepSeek, Kimi, Qwen** | Chinese labs (DeepSeek, Moonshot AI, Alibaba) | Strong open-weight models |
| **Midjourney, Stable Diffusion** | Midjourney, Stability AI | Image generation (diffusion) |

### Closed vs open-weight models

| | Closed | Open-weight |
|---|---|---|
| **Definition** | Only available through the company's app or API | Publish their trained parameters, so anyone can download, run and adapt them |
| **Examples** | GPT, Gemini, Claude | DeepSeek, Kimi, Qwen, Llama, Mistral |
| **Pros** | Usually the most capable; managed safety and updates | Cheaper, private, customizable |
| **Cons** | Cost, less control, data goes to the provider | Harder to run; safety guardrails can be removed |

### Performance gap (2026)

- Stanford's 2026 AI Index: the top closed model leads the top open one by about **3.3%**; six of the top ten models are closed; the top four companies are within 25 Elo points on the Arena leaderboard.
- Artificial Analysis (April 2026): the leading open-weight models (Kimi K2.6, MiMo V2.5 Pro, DeepSeek V4 Pro) scored within **3–6 points** of the leading proprietary models on its Intelligence Index.

### Expanded context from Research Notes (AI Search section)

**Perplexity** is described as built as an answer engine from the start, with fresh web retrieval on every query, its own index, hybrid keyword + vector search, and multi-stage reranking. It uses numbered footnotes on each claim and had the best citation accuracy in the Tow Center test.

**ChatGPT search** runs multiple web searches per prompt when search is used, but its architecture is not published. It uses inline source links, and search isn't always triggered.

**Google AI Overviews** uses custom Gemini on Google's index; may use fan-out; link chips beside the summary. Appears automatically at the top of results.

**Google AI Mode** uses custom Gemini with heavy query fan-out (many sub-searches); inline links and side panel. Conversational, multi-turn; 1B+ monthly users in 2026.

---

## 4.9 Using Generative AI Well

### Practical tips

1. **Be specific:** say the task, audience, length and format ("a 150-word summary for Year 10 students, as 3 bullet points").
2. **Give context and examples:** paste the source text, or show an example of what you want.
3. **Ask for sources and check them** (SIFT, Topic 8); use search-enabled modes for current facts.
4. **Iterate:** ask follow-ups, request changes, ask it to critique its own answer.
5. **Ask neutrally:** "What are the strongest arguments against this?" avoids sycophancy.
6. **Don't share private or sensitive information** you wouldn't want stored (Topic 11).

### Expanded context from Research Notes (Accuracy section)

**SIFT** is a quick routine professional fact-checkers use:

1. **S — Stop:** Before you trust or share an answer, pause. Do you know where this came from? Is it surprising or too perfect?
2. **I — Investigate the source:** Open the cited link. Who wrote it? Is it a real expert, an official body, a forum post, or satire?
3. **F — Find better coverage:** Search for the claim elsewhere. Do other trusted sources say the same thing?
4. **T — Trace claims to the original:** Find the original study, quote or data. Check the AI didn't change numbers, dates or meaning.

**Lateral reading** is the core skill: instead of reading one page very carefully, open new tabs and see what other sources say about that page and claim.

---

## 4.10 Adoption, Usage and Costs

### Adoption

Generative AI reached **53% adoption within three years**, faster than the PC or the internet (Stanford AI Index 2026).

### Usage patterns

NBER (2025):
- ~80% of ChatGPT messages are practical guidance, seeking information or writing
- 70%+ are non-work
- Coding is only ~4% (more in Topic 10)

### Environmental cost

Reported from the 2026 AI Index:
- AI data-center power capacity reached about **29.6 GW**, comparable to New York State's peak demand
- Training one frontier model (xAI's Grok 4) was estimated at about **72,816 tonnes of CO₂-equivalent**

This links to the sustainability principle in Topic 11.

### Expanded context from Research Notes (User Experience section)

The largest study so far, "How People Use ChatGPT" (NBER working paper by OpenAI's economic research team and Harvard economist David Deming, September 2025), analyzed a privacy-protected sample of conversations.

**Key findings:**
- **Scale:** by July 2025, about 700 million weekly users sent 18 billion messages a week, roughly 10% of the world's adults.
- **Mostly personal use:** non-work messages grew from 53% to over 70% of all usage between June 2024 and June 2025.
- **Three main topics:** practical guidance (how-to advice, tutoring, ideas), seeking information, and writing make up nearly 80% of conversations.
- **Writing leads at work:** about 40% of work messages, and most of those ask the AI to edit text the user already wrote rather than create from scratch. Coding was only about 4% of messages.
- **Asking more than doing:** about half of messages are "Asking" (advice or information to help decide something), more than "Doing" (produce an output) or "Expressing" (sharing feelings).
- **Companionship is small:** only a fairly small share of messages were about relationships or emotional topics.

---

## Try it yourself

### Activity 4.1 · Predict the next word

Write "The weather today is " and list your top 3 guesses with how likely you think each is. Then ask a chatbot to finish the sentence three times (new chat each time).

**What to notice / answers:** You just did what an LLM does: rank possible next tokens. Different answers each time show sampling and temperature.

---

### Activity 4.2 · Hallucination hunt

Ask: "Give me 3 academic papers about AI tutors in rural schools, with authors and years." Then search for each paper.

**What to notice / answers:** Count how many really exist. Fabricated sources are a known hallucination type (Topic 8).

---

## KEY TAKEAWAYS

- Generative AI creates new content; LLMs are generative models that predict the next token.
- Built in stages: pretraining (self-supervised) → Transformer with self-attention → SFT + RLHF → grounding with RAG and tools.
- Answers are generated one token at a time by probability, so they are fluent but not automatically true.
- Reasoning models think step by step; diffusion models make images by removing noise.
- Closed models still lead, but open-weight models are only a few points behind.

---

## Key terms

| Term | Definition |
|------|------------|
| **General AI** | AI that creates new content rather than labeling data. |
| **LLM** | Large language model: a big Transformer that predicts the next token. |
| **Token** | A word or piece of a word (≈ ¾ of an English word). |
| **Parameters** | The learned weights inside a model. |
| **Context window** | How many tokens the model can consider at once. |
| **Self-supervised learning** | Learning from data that supplies its own answers (the next word). |
| **Self-attention** | Each token weighing how relevant every other token is. |
| **Base model** | A pretrained model before alignment. |
| **SFT** | Supervised fine-tuning on example answers written by people. |
| **Reward model** | A model that predicts which answers humans prefer. |
| **Autoregressive** | Generating one token at a time, each based on the ones before. |
| **Temperature** | A setting controlling how random the token choices are. |
| **Open-weight model** | A model whose trained parameters are published. |
| **Diffusion model** | Image generator that learns to remove noise step by step. |
| **GAN** | Generator and discriminator networks trained against each other. |

---

## Sources (from Research Notes)

- Vaswani et al., Attention Is All You Need (2017)
- Ouyang et al., Training language models to follow instructions with human feedback (InstructGPT, 2022)
- Kalai et al. / OpenAI, Why Language Models Hallucinate (2025)
- Artificial Analysis, Recent open weights model launches (April 2026)
- Stanford HAI, 2026 AI Index Report (via secondary summaries)
- Chatterji et al., How People Use ChatGPT (NBER, 2025)
- Lewis et al., Retrieval-Augmented Generation (2020)
- Liu et al., Lost in the Middle (2023)
- Mirzadeh et al., GSM-Symbolic (Apple, 2024)
- OpenAI, Expanding on what we missed with sycophancy (2025)
- Alom et al., The History Began from AlexNet (arXiv)
- Argonne ATPESC, Intro to Deep Learning (2026)
