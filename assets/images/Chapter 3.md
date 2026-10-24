# Image Asset Register

**Project:** AI Overview study guide
**Last updated:** 2026-10-24
**Maintained by:** Taing Kuypheav

This file logs every image used across the deck. Update it the moment an image is added, replaced, or removed. If an image breaks or a source vanishes, this file is how you find the replacement.

---

## Status legend

| Status | Meaning |
|---|---|
| ✅ **Local** | Downloaded, stored in `/images`, referenced by relative path. Safe. |
| ⚠️ **Hotlinked** | Loaded from an external URL. Renders today; may break without warning. |
| 🔍 **Unverified** | Caption or content not yet checked against the actual image. |
| 🚩 **Flagged** | Known problem — AI-generated, garbled labels, expiring URL, or wrong figure. |
| ⬜ **Planned** | Needed but not yet sourced or created. |

---

## Master table

| Fig | Chapter | Subject | Status | Local file | Source page |
|---|---|---|---|---|---|
| 1 | 3 | BPE merge process | ⚠️ Hotlinked · 🔍 Unverified | `bpe-merge.webp` | [GeeksforGeeks — BPE](https://www.geeksforgeeks.org/nlp/byte-pair-encoding-bpe-in-nlp/) |
| 2 | 3 | Embedding space | ⚠️ Hotlinked · 🔍 Unverified | `embedding-space.png` | [Manela — LLM Embeddings](https://matthewmanela.com/blog/exploring-the-power-of-llm-embeddings/) |
| 3 | 3 | Positional encoding | ⚠️ Hotlinked | `positional-encoding.webp` | [GeeksforGeeks — Positional Encoding](https://www.geeksforgeeks.org/nlp/positional-encoding-in-transformers/) |
| 4 | 3 | Q/K/V projections | ⚠️ Hotlinked · 🚩 Expiring CDN | `qkv-projections.png` | [2020 ML — QKV Mechanism](https://2020machinelearning.medium.com/decoding-the-key-query-value-mechanism-in-transformer-models-thru-a-deep-discussion-with-claude-ai-2da5a66d4f8e) |
| 5 | 3 | Causal masking | ⚠️ Hotlinked | `causal-mask.png` | [Modular — LLM Step 03](https://llm.modular.com/step_03.html) |
| 6 | 3 | Training stages | ⚠️ Hotlinked · 🚩 AI-generated | `training-stages.png` | [Intelligent Tools — Demystifying LLMs](https://intelligenttools.co/blog/demystifying-large-language-models) |

---

## Asset detail

### Figure 1 — BPE merge process

- **Chapter / section:** Ch 3 → How LLMs Operate → 1. Tokens and Embeddings
- **URL:** `https://media.geeksforgeeks.org/wp-content/uploads/20260918144115070601/frame_3828.webp`
- **Alt text:** Byte pair encoding merges the most frequent adjacent character pairs into sub-word tokens
- **Caption:** Byte pair encoding builds a sub-word vocabulary by repeatedly merging the most frequent adjacent pairs.
- **Attribution:** GeeksforGeeks — "Byte Pair Encoding (BPE) in NLP"
- **Reference number:** 9
- **Notes:**
  - 🚩 Upload path contains `20260918` — a future-dated directory. It resolves now but may be a temporary CDN path.
  - 🔍 Verify the image actually shows a merge sequence (characters → pairs → words) and not a general BPE diagram.
- **Action:** Download locally; confirm content; rename to `bpe-merge.webp`.

### Figure 2 — Embedding space

- **Chapter / section:** Ch 3 → How LLMs Operate → 1. Tokens and Embeddings
- **URL:** `https://matthewmanela.com/wp-content/uploads/2023/10/image-3.png`
- **Alt text:** Embedding space in which words with similar meanings are positioned close together
- **Caption:** Embeddings represent tokens as vectors in a multi-dimensional space, where proximity encodes similarity of meaning.
- **Attribution:** Matthew Manela — "Exploring the Power of LLM Embeddings"
- **Reference number:** 10
- **Notes:**
  - 🔍 Caption was written from the *article's topic*, not from the image itself. The filename `image-3.png` gives no clue.
  - If it shows the king/queen parallelogram, say so — it's the most recognisable visual in the field. If it shows Word2Vec clusters or a contextual-embedding comparison, rewrite the caption to match.
- **Action:** Open the image; rewrite caption to describe what is actually depicted; download locally.

### Figure 3 — Positional encoding

- **Chapter / section:** Ch 3 → How LLMs Operate → 2. The Transformer and Self-Attention
- **URL:** `https://media.geeksforgeeks.org/wp-content/uploads/20250818131508982635/positional_encoding_in_transformer.webp`
- **Alt text:** Positional encoding adds a position signal to each token embedding
- **Caption:** Positional encoding injects a position signal into each token's embedding, so the model can tell "dog bites man" from "man bites dog".
- **Attribution:** GeeksforGeeks — "Positional Encoding in Transformers"
- **Reference number:** 11
- **Notes:**
  - Placement sits before the concept is fully used. Consider adding one bridging clause to the preceding paragraph: *"Without this signal, 'dog bites man' and 'man bites dog' would produce identical attention scores."*
- **Action:** Download locally; confirm it shows the position signal (heat-map or vector diagram), not the full transformer block.

### Figure 4 — Q/K/V projections

- **Chapter / section:** Ch 3 → How LLMs Operate → 2. The Transformer and Self-Attention → Step 1
- **URL:** `https://miro.medium.com/v2/resize:fit:1200/1*6JpXMLrsmNcf8-x3aV2Tvg.png`
- **Alt text:** The same input vector projected three ways into query, key, and value vectors
- **Caption:** One input vector is projected three ways — query, key, and value — using three separately learned weight matrices.
- **Attribution:** 2020 Machine Learning — "Decoding the Key, Query, Value Mechanism in Transformer Models"
- **Reference number:** 12
- **Notes:**
  - 🚩 The URL contains `resize:fit:1200` — a Medium CDN transform parameter. These can change or expire, and the image you see may be a resized copy rather than the original.
- **Action:** Download the highest-resolution version available; store locally. This is the most fragile URL in the set.

### Figure 5 — Causal masking

- **Chapter / section:** Ch 3 → How LLMs Operate → 2. The Transformer and Self-Attention → Causal masking
- **URL:** `https://llm.modular.com/images/causal-masking-light.png`
- **Alt text:** A causal mask blocks each token from attending to future positions
- **Caption:** The causal mask zeroes out attention to future tokens, so token 5 can see tokens 1–5 but not token 6.
- **Attribution:** Modular — "LLM Step 03"
- **Reference number:** 13
- **Notes:**
  - Filename ends in `-light`, implying a light-mode variant exists. If the deck is ever viewed in dark mode, check readability.
  - Confirm the image is the triangular attention mask itself, not a diagram of the *pipeline step* that introduces masking.
- **Action:** Download locally; if a dark-mode variant exists, note its URL here.

### Figure 6 — Training stages

- **Chapter / section:** Ch 3 → How LLMs Operate → 3. Training
- **URL:** `https://github.com/user-attachments/assets/5bfae9c4-9fea-472c-ac15-271479c0e1e3`
- **Alt text:** A pipeline of the training stages an LLM passes through
- **Caption:** Modern LLMs are trained in stages — pretraining, post-training, and reasoning-focused reinforcement learning — each with a different training signal.
- **Attribution:** Intelligent Tools — "Demystifying Large Language Models"
- **Reference number:** 14
- **Notes:**
  - 🚩 **Highest-risk asset in the set.** The original filename was `Gemini_Generated_Image_s7kdtts7kdtts7kd.png` — the diagram was generated by an image model. AI-generated diagrams routinely contain garbled labels, misspelled stage names, and reversed arrows.
  - The figure sits directly above a three-row table defining the stages. If the diagram's labels disagree with the table, the contradiction is visible on the same screen.
  - GitHub attachment URLs are tied to a repository. If the repo or attachment is deleted, the figure breaks silently in any exported copy.
  - ⚠️ Renders at 2816×1536 — enormous at full width. Needs a width constraint (HTML `width="800"` or a locally resized copy).
- **Action:** Read every label in the image against the chapter's table. If inaccurate, replace with a hand-built three-box diagram. Then download locally.

---

## Planned assets (not yet sourced)

These were recommended for Chapter 3 but are not in the file. Track them here so they don't get lost.

| Fig | Subject | Section | Notes |
|---|---|---|---|
| ⬜ TBD | "It" coreference attention trace | 2. Self-Attention | Lines or heat-map showing "it" → "animal". Most effective single visual for self-attention. |
| ⬜ TBD | Causal mask triangular matrix | 2. Self-Attention | Alternative to Fig 5 if that image turns out to be the wrong thing. |
| ⬜ TBD | RLHF loop | 3. Training | Model generates → humans rank → reward model learns → LM tuned. |
| ⬜ TBD | RLVR loop | 3. Training | Same cycle, but reasoning trace stripped before the checker sees only the final answer. |
| ⬜ TBD | Autoregressive sampling loop | 4. Inference | Circular diagram, three iterations side by side. |
| ⬜ TBD | Temperature: sharp vs. flat distribution | 4. Inference | Makes non-determinism visible. |
| ⬜ TBD | Context window as a bounded desk | 4. Inference | Prompt + documents + history + response inside a hard boundary. |
| ⬜ TBD | RAG architecture | Worked Example / bridge to Ch 4 | Offline indexing pipeline + online query pipeline. Should be the final image in Ch 3. |

Mermaid can reproduce the BPE flowchart, the training pipeline, the RLHF/RLVR loops, the autoregressive loop, and the RAG architecture natively — no external image or URL dependency.

---

## Housekeeping rules

**File naming.** Lowercase, hyphenated, descriptive: `bpe-merge.webp`, not `frame_3828.webp`. Numbering (`fig-01-...`) is optional but makes sorting predictable.

**Storage.** Once downloaded, store in `/images` beside the `.md` and reference relatively:

```markdown
![Alt text](./images/bpe-merge.webp)
```

Relative paths survive export, zipping, and moving the folder. External URLs do not.

**Alt text.** Written for someone who cannot see the image. Describe what it *shows*, not what it's *about*.

**Captions.** Describe the specific content, then attribute. Pattern:

> *Figure N. [What this specific image depicts]. Image: [Source name](link).*

**Attribution and fair use.** Every asset here is hotlinked from a third party — GeeksforGeeks, Medium, Modular, a personal blog, and a commercial site. For an internal or educational deck this is normally defensible, but record the source for every image so attribution can be added or permission sought if the deck is ever published or distributed. Note the licence for each source here if you check it.

**Verification discipline.** An image marked 🔍 has a caption written from assumption, not inspection. Clear the 🔍 by opening the image and confirming the caption matches. Do this before final review, not after.

**When an image breaks.** Don't silently swap the URL. Update the URL, the alt text if the content changed, the caption if the depiction changed, and the reference list entry. Then note the change here with a date.

---

## Change log

| Date | Fig | Change |
|---|---|---|
| 2026-10-24 | — | Register created; Figs 1–6 logged. |
| 2026-10-24 | 6 | Markdown image syntax fixed (HTML `<img>` had been pasted inside Markdown parentheses). |
