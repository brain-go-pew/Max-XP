# AI Usage Log — AI Overview Study Guide

**10/21/2026**
# AI Usage Log

**Project:** AI Overview study guide (group project)
**Session date:** 2026-10-24 (single session; individual timestamps not recorded)
**Tool:** Deepseek with Deepthink and Search
**Purpose of this log:** Record all substantive prompts used in this project, for transparency, reproducibility, and process review.

**Most, if not all, of the prompting I have done includes the use of Deepseek with the Deepthink and Search functions on.**
---

## Summary

| # | Phase | Prompt (abbreviated) | Output produced |
|---|---|---|---|
| P01 | Admin | What to write in a group project log after a meeting | Template + worked example for project log |
| P02 | Architecture | Review of initial table of contents | Structural feedback: gaps, ordering, naming |
| P03 | Architecture | Review of revised table of contents | Second-round feedback: ordering fixes, consistency, missing elements |
| P04 | Architecture | What should every chapter contain? | Standard chapter template + per-chapter additions |
| P05 | Content | Elaborate Topics 3 & 4 using only sourced information | Sourced draft of Chapter 3 and Chapter 4 |
| P06 | Content | Elaborate further; technical wording allowed | Expanded technical draft |
| P07 | Revision | Add plain-English version of every explanation | Two-layer draft (Plain English + Going deeper) |
| P08 | Revision | "Going deeper" sections are too complex | Diagnosis of why they failed |
| P09 | Revision | Keep content, simplify "Going deeper" only | Full revised draft with simplified technical layers |
| P10 | Learning | Knowledge check questions pasted | Model answer key with marking criteria |
| P11 | Learning | Own-words answers submitted for marking | Graded feedback with corrections |
| P12 | Learning | Concern about being the target audience and not understanding | Diagnostic response linking comprehension gaps to deck design |
| P13 | Review | Chapter 4 file uploaded + "who even uses bing" critique | Structural diagnosis of the chapter |
| P14 | Content | Rewrite Chapter 4 around AIs people actually use, including minor tools | Full rewritten Chapter 4 |
| P15 | Formatting | Cite all sources per chapter in AMA format | Per-chapter reference lists in AMA 11th edition |
| P16 | Production | Chapter 3 file uploaded + reorganize into .md with references | Formatted .md chapter |
| P17 | Assets | What images should Chapter 3 include? | Image plan mapped to chapter sections |
| P18 | Assets | Insert images (batch 1, with URLs and source links) | Chapter 3 .md with Figures 1–2 |
| P19 | Assets | Insert images (batch 2: QKV, causal mask, positional encoding, training stages) | Chapter 3 .md with Figures 3–6 |
| P20 | Assets | Fix malformed image markdown | Corrected syntax options |
| P21 | Assets | Log all image assets in a separate .md file | Image asset register |
| P22 | Admin | Gather all prompts used in this conversation into a .md file | This document |

---

## Detailed entries

### Phase 1 — Admin

#### P01
> We have a group meeting and now i have to write the results of that group project inside the project log. What should i write?

**Output:** A template (meeting details, discussion summary, results, action items, next steps) plus a filled-in example entry and writing tips.

---

### Phase 2 — Study guide architecture

#### P02
> We're creating a study guide to teach average people about ai (AI Overview). This are the topics we decided on. What improvements should be made to this table of content?
>
> AI Overview
> The Big Picture — what AI Overviews are and why they exist
> From Links to Answers — how search evolved to this point
> Who's Playing — Google, Perplexity, Bing, ChatGPT and how they differ
> Under the Hood — the pipeline from query to cited answer
> Making It Accurate — grounding, hallucination control, source conflicts
> Measuring Quality — how you know an overview is good
> The User Experience — design, trust signals, edge cases
> Risks & Responsibilities — bias, publishers, misinformation, regulation
> The Business Side — SEO shifts, monetisation, market dynamics
> My Project & Wrap-Up
> Conclusion & Takeaways (10 slides)
> Google Form Assessment

**Output:** Structural feedback — missing "how to use it" chapter, missing AI literacy foundations, glossary needed, assessment too end-loaded, overlapping chapters, suggested revised order.

#### P03
> AI Overview
> The Big Picture — what AI Overviews are and why they exist
> From Links to Answers — how search evolved to this point
> AI Fundamentals – What are llms? How do they operate? Capabilities?
> Who's Playing — Google, Perplexity, Bing, ChatGPT and how they differ
> Under the Hood — the pipeline from query to cited answer
> Using It Well — query strategies, verifying claims, when to trust the citations.
> Making It Accurate — grounding, hallucination control, source conflicts
> Measuring Quality — how you know an overview is good
> Limitations & Failure Modes – When ai gets it wrong
> The User Experience — design, trust signals, edge cases, Accessibility & inclusivity
> Risks & Responsibilities — bias, publishers, misinformation, regulation, privacy, user data
> The Business Side — SEO shifts, monetisation, market dynamics
> My Project & Wrap-Up
> Conclusion & Takeaways (10 slides)
> Key terms (Glossary; grounding, hallucination, RAG, citation, SERP, etc)
> Google Form Assessment (Final version, should have small knowledge checks every chapter)

**Output:** Second-round feedback — reorder accuracy → limitations → quality → using-it-well; move AI Fundamentals up; fix capitalisation and dash consistency; resolve the two-endings problem; make assessment structure explicit.

#### P04
> what should we include every chapter of study guide?

**Output:** A standard nine-part chapter template (title, learning objectives, why it matters, key terms, core content, worked example, recap, knowledge check, bridge) plus a table of chapter-specific additions and consistency rules.

---

### Phase 3 — Content drafting

#### P05
> Ok, I'm doing topics 3 & 4: AI Fundamentals – What are llms? How do they operate? Capabilities? & Who's Playing — Google, Perplexity, Bing, ChatGPT and how they differ. Elaborate on everything I need to know about these topics. Do not create your own information. Use existing information from the internet and cite the sources you used (give specific citations and links).

**Output:** First sourced draft of Chapters 3 and 4, with inline citations and a numbered source list.

#### P06
> Keep the topics you made in heading 3. However, elaborate further on all the information you provided for each sub-topic. The amount of information provided is not enough. Use technical wording wherever possible but keep it readable for the audience. No worries about length or complexity because I will proof-read it myself.

**Output:** Expanded technical version of both chapters — attention formula, training stages, retrieval architectures, citation-overlap data.

---

### Phase 4 — Revision for readability

#### P07
> The usage of technical wording makes the reading tedious as the readers constantly have to check the key terms. Make sure that, whatever is being explained, has a "dumbed down" version of the explanation.

**Output:** Two-layer draft: Plain English explanation (with analogy) followed by Going deeper (technical detail), plus a plain-first key terms table.

#### P08
> For the "going deeper" sections, they are pretty complex. I'm not even sure if I understand them

**Output:** Diagnosis of four specific failure modes in the technical sections (stacked clauses, undefined terms, no worked walkthrough, citations interrupting flow), plus four rewritten sample sections to a new standard.

#### P09
> nono keep the previous response's contents but just change the "going deeper" parts to be a bit more easy to follow.

**Output:** Full chapter draft with contents unchanged and all Going deeper blocks rewritten: one idea per sentence, terms defined at point of use, mechanisms traced step by step.

---

### Phase 5 — Learning and verification

#### P10
> Knowledge check
> Recall: What is an LLM's core training objective?
> Application: Why might an LLM confidently answer a question about a recent event incorrectly?
> Compare: What is the difference between pretraining and post-training?
> Evaluate: A chatbot gives a fluent, well-structured answer with no sources. Why should you not automatically trust it?

**Output:** Model answer key with "must contain" marking criteria and common wrong answers for each question.

#### P11
> I'm going to quesiton/explain things in my own words:
> Recall: To predict the most likely to-be next token.
> Application: It's training dataset didn't include that recent event so it has information cutoff. In that case, it will simply find closely matching tokens and generate text without context. Therefore, it sounds confident but ultimately, it's just saying random things
> Compare: Pretraining gives the LLM an enormous amount data that teaches it how to encode human languages, meanings, ... Post-training is when it's fed human-corrected responses that shows it what humans expect from a response. The LLM is also given rewards (or given weights) when it gives the correct response from it's own reasoning. The reasoning itself isn't given any rewarding or kept at all because it will sway the AI's probabilities of picking later tokens.
> Evaluate: idk

**Output:** Marked feedback — Recall correct; Application corrected ("plausible," not "random"); Compare corrected (RLHF missing, reasoning-stripping rationale wrong); Evaluate supplied with a three-reason model answer.

#### P12
> ok im basically the audience of this whole ppt. The fact that I'm not understanding this and answering the knowledge check correctly is pretty bad

**Output:** Reframing of the result as diagnostic data about the deck rather than about the reader; identified mis-calibrated question laddering; recommended a running confusion log.

---

### Phase 6 — Chapter 4 rewrite

#### P13
> [Attachment: Chapter 4 — Who's Playing Google, Perplexity,.txt]
> who even uses bing lmao? This chapter is a bit crooked

**Output:** Structural diagnosis — Bing included without justification; chapter is a product directory with no argument; learning objective 4 never delivered; missing comparison table, worked example, recap, and checks. Plus four accuracy fixes (Microsoft Graph conflation, missing Sonar, mixed citation units, undated statistics).

#### P14
> Simply make this chapter about AIs are people actually use and explain everything there is to know about them. Include some main AIs and some more minor Ais.

**Output:** Fully rewritten Chapter 4 — major platforms (ChatGPT, Gemini, Claude, Copilot, Meta AI) and minor/niche tools (Perplexity, DeepSeek, Grok, Le Chat, Pi, long tail), with dated statistics, comparison table, worked example, and laddered knowledge checks.

---

### Phase 7 — Citations and formatting

#### P15
> Cite all the sources for each chapter in AMA format (and put them in separate sections). These are to be put at the bottom of each chapter respectively.

**Output:** Per-chapter AMA 11th edition reference lists (Ch 3; Ch 4 current version; Ch 4 earlier draft), plus a verification note flagging reconstructed entries and weak sources.

#### P16
> [Attachment: Chapter 3. LLM Fundamentals.txt]
> I've changed my chapter 3 title to LLM fundamentals. Given here is the content. Add the references at the bottom of the chapter. Organize all the information, add proper elements (headers, tables, ...) into the contents. Make it suitable to be contained in a .md file.

**Output:** Chapter 3 formatted as a complete `.md` file — consistent heading hierarchy, key-terms table, capability and limitation tables, training-stage table, model answers, AMA references.

---

### Phase 8 — Image assets

#### P17
> What images should I include for chapter 3?

**Output:** Image plan mapped to chapter sections — BPE merge process, embedding parallelogram, Q/K/V projections, self-attention trace, causal mask, positional encoding, training pipeline, RLHF/RLVR loops, autoregressive loop, context window, RAG architecture — plus sourcing notes.

#### P18
> I need to add images into the chapter 3 .md file. The following will be (paragraph before image is added) -- (url of img that is added) -- (link of that image).
> [Paragraph on BPE] — https://media.geeksforgeeks.org/.../frame_3828.webp — https://www.geeksforgeeks.org/nlp/byte-pair-encoding-bpe-in-nlp/
> [Paragraph on embeddings] — https://matthewmanela.com/wp-content/uploads/2023/10/image-3.png — https://matthewmanela.com/blog/exploring-the-power-of-llm-embeddings/

**Output:** Chapter 3 .md with Figures 1–2 inserted in the specified format, captioned and attributed; sources added as references 9–10.

#### P19
> The names are a useful metaphor... [QKV paragraph] — https://miro.medium.com/... — https://2020machinelearning.medium.com/...
> Causal masking... [paragraph] — https://llm.modular.com/images/causal-masking-light.png — https://llm.modular.com/step_03.html
> The model does this in many layers... [positional encoding paragraph] — https://media.geeksforgeeks.org/.../positional_encoding_in_transformer.webp — https://www.geeksforgeeks.org/nlp/positional-encoding-in-transformers/
> Modern LLMs go through multiple training stages: — https://wmpyxajsoiwnvxkmfqty.supabase.co/.../Gemini_Generated_Image_s7kdtts7kdtts7kd.png — https://intelligenttools.co/blog/demystifying-large-language-models

**Output:** Chapter 3 .md with Figures 3–6 inserted, captioned and attributed; sources added as references 11–14.

#### P20
> fix this: ![A pipeline of the training stages an LLM passes through](<img width="2816" height="1536" alt="image" src="https://github.com/user-attachments/assets/5bfae9c4-9fea-472c-ac15-271479c0e1e3" />#)
> *Figure 6. Modern LLMs are trained in stages...*

**Output:** Diagnosis (HTML `<img>` pasted inside Markdown image parentheses) and two corrected replacements — standard Markdown, or HTML with a width constraint.

#### P21
> Need to log all my image assets in another .md file...

**Output:** Image asset register — status legend, master table, per-asset detail (URL, alt text, caption, attribution, reference number, risk notes, action), planned assets, housekeeping rules, change log.

---

### Phase 9 — Meta

#### P22
> Gather together all the important prompts I have used in this conversation so I can log my ai usage. This needs to be put in .md file

**Output:** This document.

---

## Patterns and notes

**Iterative refinement, not one-shot generation.** No substantive artifact was produced in a single prompt. Chapters 3 and 4 each went through three or more rounds: sourced draft → technical expansion → readability revision → format conversion. The quality gains came from the corrective prompts (P07–P09, P13, P20), not the initial requests.

**The most effective corrective prompts named the problem precisely.** P07 ("readers constantly have to check the key terms"), P08 ("I'm not even sure if I understand them"), and P13 ("who even uses bing") each produced sharper revisions than a general "improve this" would have. The critique carried the diagnosis.

**The author's own confusion functioned as a design review.** P11 and P12 — a failed knowledge check and the admission of being the target audience — produced the most useful structural finding in the session: that the questions were mis-calibrated, not the reader. This is logged as a reminder that self-testing is a legitimate review instrument.

**Files were used as the handoff format.** From P13 onward, each round began with an uploaded `.md` or `.txt` rather than a pasted excerpt. This reduced transcription errors and kept revisions anchored to a stable version.

---

## Reusable prompt patterns

Extracted from this session for future use.

1. **Sourced-only elaboration.** "Do not create your own information. Use existing information from the internet and cite the sources you used (give specific citations and links)."
2. **Two-layer explanation.** "Whatever is being explained must have a dumbed-down version of the explanation."
3. **Scoped revision.** "Keep the previous response's contents but just change [specific section]."
4. **Audience-as-reviewer.** "I'm basically the audience — if I don't understand it, the deck doesn't work."
5. **Per-chapter citation.** "Cite all sources for each chapter in AMA format, in separate sections at the bottom of each chapter."
6. **Asset handoff.** "(paragraph before image) — (image URL) — (source link)" as a repeatable insertion format.
7. **Self-test as review.** Answer the chapter's own knowledge checks and log where you fail; treat failures as deck defects first, comprehension gaps second.
**Student/Team:** Max-XP
**AI Tool Used:** Gemini (or whichever AI assistant you are using)
**Purpose:** Assisting with GitHub repository setup, formatting Markdown files, structuring the Project Plan, and organizing the team workflow based on provided images and instructions.

---


**10/23/2026**
## Interaction 1: Initial Repository Setup & Structure
- **Prompt Used:** 
  > *[Uploaded "1. General Instructions.txt"]* "yo, need to do a github repo to document all my work in a project to create study material teaching people about AI overview. This are the instructions for the github repo. I am not experienced using github at all. I don't really know whats happening but I do have basically all the information in one place already. I just don't know where to put it:"
- **AI Response Summary:** The AI broke down the assignment requirements into a step-by-step guide for beginners, explaining how to create a repository, structure folders, and map existing content into Markdown files.
- **Verification/Action Taken:** I followed the step-by-step instructions to create the actual GitHub repository and folders.

---

## Interaction 2: Drafting the Initial README
- **Prompt Used:** 
  > "retain all this information. For now, help build the README file. Use 7 placeholder names for the team names, their role, experience and strengths. Project purpose and intended Learners are in seperate sections. The location of materials should be structured nicely. As for the structure of the content, I will need to create all the .md files of every required document first so no need to do it."
- **AI Response Summary:** The AI generated a complete `README.md` template with tables for team members, separate sections for Project Purpose and Intended Learners, and a clear "Location of Materials" table.
- **Verification/Action Taken:** I customized the placeholder names with my actual team members' information later.

---

## Interaction 3: Rewriting README & Generating Module Outline
- **Prompt Used:** 
  > *[Uploaded README text and screenshot of GitHub repo structure]* "Here is my readme.md file. Here is the structure of the repo (assets still missing because Idk how to create). Still missing internal deadlines/time table. We also have a table of content already to fit inside the module outline.md. You will now rewrite the readme.md to replace and update content appropriately. Also, write the module outline document with the table of content provided: [Inserted Table of Contents]"
- **AI Response Summary:** The AI updated the README to match my actual GitHub folder structure, explained how to create missing `assets` folders using `.gitkeep`, and generated the `Module Outline.md` file using my exact Table of Contents.
- **Verification/Action Taken:** I used the instructions to create the `.gitkeep` files and pasted the Module Outline into my repository.

---

## Interaction 4: Project Plan (Audience, Goals, Timeline, Meetings, Risks)
- **Prompt Used:** 
  > *[Uploaded 3 images containing meeting schedules, timelines, and risks]* "I have to move the intended audeince, learning goals to project plan. Additionally, generate (code for the project plan.md) a timeline structure like in the image shown, meeting organization plans, main risks and solutions. that is all for now. Make sure to only use the wording and info from the images provided."
- **AI Response Summary:** The AI extracted the text from my images to create the Timeline, Meeting Schedule, and Risk tables. It also formatted the Intended Audience and Learning Goals into the `Project Plan.md`.
- **Verification/Action Taken:** I verified that the AI only used the exact wording from my images, then committed the file to GitHub.

---

## Interaction 5: Generating Detailed Plans for PPT, Video, Lecture, and Markdown
- **Prompt Used:** 
  > "Continuing on, generate sections to provide a detailed plan for the ppt, Video tutorial, shared markdown content (everything to know about the markdown contents (you will also write a detailed chapter on this.), live mini lecture, and a master to-do list. Information about those sections are shown: [Inserted detailed info about PPT, Study Guide, Video Parts 1-3]"
- **AI Response Summary:** The AI wrote detailed plans for the PPT, Video, and Mini-Lecture, generated a comprehensive guide for what the Shared Markdown Content should include, and created a 23-task Master To-do List.
- **Verification/Action Taken:** I reviewed the plans and added them to the `Project Plan.md`.

---

## Interaction 6: Clarifying Task Numbers (T18-T23)
- **Prompt Used:** 
  > "What is t18...T23 ??"
- **AI Response Summary:** The AI explained that it generated tasks T18-T23 based on the Stage 3 deadlines and risk mitigation strategies from the images I uploaded.
- **Verification/Action Taken:** I confirmed the tasks made sense and kept them in the Master To-do List.

---

## Interaction 7: Resolving GitHub Merge Conflict
- **Prompt Used:** 
  > "There is a conflict: [Pasted GitHub conflict error text] I cant merge into main"
- **AI Response Summary:** The AI explained what a Git merge conflict is, explained why it happened (teammates editing the same table), and provided a clean, merged version of the Team table. 
- **Verification/Action Taken:** I deleted the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), pasted the clean table, and successfully merged my branch into `main`.

---

## Interaction 8: Organizing Study Guide Folders
- **Prompt Used:** 
  > "Make a folder to contain each chapter of my table of contents."
- **AI Response Summary:** The AI provided a numbered folder structure and step-by-step instructions on how to use GitHub to create these folders by adding a `chapter-XX.md` file inside each one.
- **Verification/Action Taken:** I followed the instructions to create the folders and files in the `Study Guide` directory of the repository.

---

## General Declaration
I confirm that the AI was used as a planning, formatting, and structural assistant. All core content, team roles, and specific project requirements were provided by me and my team. The AI did not write the educational content for the chapters, but it helped organize the framework and plan for how we will write them.
