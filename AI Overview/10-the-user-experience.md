# 10 The User Experience

How people actually use AI, and how design shapes whether they trust it the right amount.

---

## 10.1 How People Actually Use AI

### "How People Use ChatGPT" (NBER working paper, September 2025)

OpenAI economists + Harvard's David Deming:

| Finding | Detail |
|---------|--------|
| **Scale** | ~700 million weekly users sending 18 billion messages a week by July 2025, ~10% of the world's adults. |
| **Mostly personal** | Non-work messages grew from 53% to 70%+ (June 2024 → June 2025). |
| **Three main topics** | Practical guidance, seeking information and writing make up nearly 80%. |
| **Writing leads at work** | ~40% of work messages, mostly editing the user's own text. |
| **Coding** | Only ~4%. |
| **Asking > Doing > Expressing** | About half of messages are "Asking." |
| **Companionship** | Small: few messages are about relationships or emotions. |

### Implication

Most people use AI as an **advisor and smarter search engine**, so design must support decisions: clear answers, trustworthy sources, honest limits.

### Expanded context from Research Notes

The largest study so far, "How People Use ChatGPT" (NBER working paper by OpenAI's economic research team and Harvard economist David Deming, September 2025), analyzed a privacy-protected sample of conversations.

**Key findings:**

- **Scale:** by July 2025, about 700 million weekly users sent 18 billion messages a week, roughly 10% of the world's adults.
- **Mostly personal use:** non-work messages grew from 53% to over 70% of all usage between June 2024 and June 2025.
- **Three main topics:** practical guidance (how-to advice, tutoring, ideas), seeking information, and writing make up nearly 80% of conversations.
- **Writing leads at work:** about 40% of work messages, and most of those ask the AI to edit text the user already wrote rather than create from scratch. Coding was only about 4% of messages.
- **Asking more than doing:** about half of messages are "Asking" (advice or information to help decide something), more than "Doing" (produce an output) or "Expressing" (sharing feelings).
- **Companionship is small:** only a fairly small share of messages were about relationships or emotional topics.

**Why it matters.** Most people use AI as an advisor and a smarter search engine, not just a robot that does tasks. So the user experience must support decisions: clear answers, trustworthy sources, and honest limits.

**Example.** A student asks for a study plan for exams (practical guidance), checks a definition (seeking information), and asks for feedback on an essay draft (writing), all in one week.

---

## 10.2 Design Principles

AI is probabilistic, sometimes wrong, and changes over time, so it needs special design rules.

### Microsoft's 18 Guidelines for Human-AI Interaction (2019)

Condensed from 150+ recommendations and tested with 49 designers on 20 AI products:

| Stage | Example guidelines |
|-------|-------------------|
| **Initially** | Make clear what the system can do, and how well (how often it may be wrong) |
| **During interaction** | Time services to context; show relevant info; match social norms; avoid social biases |
| **When wrong** | Easy to call up, dismiss and correct; when unsure, narrow scope or ask a clarifying question; explain why |
| **Over time** | Learn from behavior; update cautiously; encourage feedback; give global controls; notify of changes |

### Google PAIR's People + AI Guidebook (six chapters)

1. User needs + defining success (does this need AI?)
2. Data collection + evaluation
3. Mental models
4. Explainability + trust
5. Feedback + control
6. Errors + graceful failure

### Shared idea

**Plan for the AI being wrong and make recovery easy.**

### Example

Email autocomplete appears only while you type, one key accepts it, typing on dismisses it, and it never changes text without you.

### Expanded context from Research Notes

AI behaves differently from normal software: it is probabilistic, sometimes wrong, and can change over time. Designers need special rules for it. Two widely used guides:

**Microsoft's 18 Guidelines for Human-AI Interaction (2019)** — Condensed from 150+ design recommendations and tested with 49 designers on 20 popular AI products. They're grouped by when they apply:

| Stage | Example guidelines |
|-------|-------------------|
| **Initially** | Make clear what the system can do; make clear how well it can do it (how often it may be wrong) |
| **During interaction** | Time services based on context; show contextually relevant information; match social norms; avoid social biases |
| **When wrong** | Make it easy to call up, dismiss and correct the AI; when unsure, narrow the scope or ask a clarifying question; explain why it did what it did |
| **Over time** | Learn from user behavior; update cautiously; encourage granular feedback; give users global controls; notify users about changes |

**Google PAIR's People + AI Guidebook** — Written for product teams, with six chapters: user needs + defining success (does this problem even need AI?), data collection + evaluation, mental models (help users understand how the AI works), explainability + trust, feedback + control, and errors + graceful failure.

**Why it matters.** These guidelines turn vague goals like "build trust" into concrete design choices. A key shared idea: plan for the AI being wrong, and make recovery easy.

**Example.** Email autocomplete follows several guidelines at once: it appears only while you type (timing), you accept it with one key or ignore it by typing on (easy invocation and dismissal), and it doesn't change your text without you.

---

## 10.3 Trust Signals and Calibrated Trust

The goal is **calibrated trust**: relying on AI when it's right and doubting it when it's wrong.

**Dangers:** overtrust (automation bias) and undertrust.

### Trust signals

| Signal | What it shows | Watch out |
|--------|---------------|-----------|
| **Citations / links** | Where a claim came from | Few people click; links may not support the claim |
| **Confidence / uncertainty** | "I'm not sure," scores, hedges | Users over-follow high-confidence answers, even wrong ones |
| **Explanations** | Why the AI answered this | Can increase blind trust |
| **Disclosure labels** | "AI-generated," "may contain mistakes" | Ignored once familiar |
| **Showing steps** | Searches run, reasoning | Long output people skim |

### The problem with explanations

Explanations can backfire: people accept AI advice more often with an explanation, right or wrong.

### The problem with confidence scores

Confidence scores cut both ways (AAAI 2026): users accept wrong high-confidence answers and reject accurate low-confidence ones.

### What works

**Cognitive forcing** (answer first, then see the AI) reduced overreliance most, but users liked it least.

### Reality check

People rarely check: Pew found links inside AI summaries clicked in only **1%** of visits.

### Design implication

Add friction that matches the stakes: light for a movie pick, strong for medical or legal decisions.

### Example

A medical AI shows its suggestion only after the doctor enters their own diagnosis.

### Expanded context from Research Notes

The goal isn't maximum trust; it's **calibrated trust**: relying on AI when it's right and doubting it when it's wrong. Google's PAIR guidebook says users shouldn't trust an AI system completely, because it's based on probability. The two dangers:

- **Overtrust (automation bias):** accepting AI output without checking, even when it's wrong.
- **Undertrust:** ignoring AI even when it's helpful, wasting its value.

**Common trust signals in AI products:**

| Signal | What it shows | Watch out |
|--------|---------------|-----------|
| **Citations / source links** | Where a claim came from, so users can check | Few people click; links may not support the claim |
| **Confidence or uncertainty** | "I'm not sure," scores, or hedged wording | Users over-follow high-confidence answers, even wrong ones |
| **Explanations** | Why the AI gave this answer | Can increase blind trust instead of reducing it |
| **Disclosure labels** | "AI-generated," "may contain mistakes" | Easily ignored once familiar |
| **Showing work / steps** | Search queries run, reasoning steps | Long output people skim |

**What research shows:**

- **Explanations can backfire:** several studies found explanations made people accept AI advice more often, whether or not it was correct; people treat an explanation as a general sign of competence.
- **Confidence scores cut both ways:** a 2026 AAAI study found users were more likely to accept high-confidence AI recommendations even when wrong, and to reject accurate ones shown with low confidence.
- **Cognitive forcing helps but is unpopular:** designs that make users think first (for example, answering before seeing the AI's suggestion) reduced overreliance the most, but users rated them least favorably.
- **People rarely check:** Pew found users clicked a link inside Google's AI summary in only 1% of visits.

**Why it matters.** Trust signals only work if they change what people do. Good design adds the right amount of friction for the stakes: light for a movie recommendation, strong for medical or legal decisions.

**Example.** A medical AI shows its suggestion only after the doctor enters their own diagnosis, then highlights where they disagree. Slower, but it prevents rubber-stamping.

---

## 10.4 Interaction Styles

| Style | Example | Strengths | Weaknesses |
|-------|---------|-----------|------------|
| **Chat** | ChatGPT, Claude, Gemini | Flexible; follow-ups | Blank-box: must know what to ask |
| **Inline** | Autocomplete, AI Overviews | No new app; in context | Intrusive; easy to accept unchecked |
| **Voice** | Siri, Alexa, voice mode | Hands-free, accessible | Hard to show sources; emotional bonding |
| **Multimodal** | Camera: "what is this?" | Understands photos, screens | Errors on complex images, charts |
| **Agents** | AI that books, shops, codes | Saves multi-step effort | Real consequences; needs approvals |

### Helpful patterns

- Suggested prompts
- Editable outputs
- Undo and confirmation before irreversible actions
- Memory controls
- Feedback buttons

### Agents need special care

Agents fail ~1 in 3 structured tasks, so a travel agent AI should stop and show a summary (dates, price, card) before paying.

### Expanded context from Research Notes

AI now reaches people through several kinds of interface, each with trade-offs:

| Style | Example | Strengths | Weaknesses |
|-------|---------|-----------|------------|
| **Chat (text)** | ChatGPT, Claude, Gemini | Flexible; follow-up questions; easy to review | Blank-box problem: users must know what to ask |
| **Inline / embedded** | Autocomplete, AI Overviews, "summarize" buttons | No new app to learn; appears in context | Can feel intrusive; easy to accept without checking |

**Helpful patterns:** suggested prompts, editable outputs, undo and confirmation before irreversible actions, memory controls, feedback buttons.

**Agents need special care:** agents fail about 1 in 3 structured tasks, so a travel agent AI should stop and show a summary (dates, price, card) before paying.

---

## 10.5 Accessibility

AI turns one kind of information into another:

| Disability | AI capability |
|------------|---------------|
| Vision | Describing photos, screens |
| Hearing | Live captions |
| Speech/motor | Voice control, non-standard speech |
| Cognitive | Simplifying, reading aloud |
| Language | Real-time translation |

### Be My Eyes "Be My AI" (2023)

Built on OpenAI's GPT-4 vision: blind and low-vision users take a photo and get a spoken description, then ask follow-ups. In beta, 16,000 users requested ~25,000 descriptions a day. Now used in Microsoft's Disability Answer Desk and on Windows.

### Risks

- Errors no one can catch (Be My Eyes keeps human volunteers)
- Inaccessible AI tools
- Privacy of photos

### Best practice

Build with disabled users, keep a human fallback, state uncertainty.

### Expanded context from Research Notes

AI can remove barriers for people with disabilities by turning one kind of information into another: images into words, speech into text, text into speech, complex text into simple text.

**How AI helps:**

- **Vision:** describing photos, scenes, labels and screens for blind and low-vision users.
- **Hearing:** live captions and transcripts from speech recognition.
- **Speech and motor:** voice control and dictation instead of typing; tools that understand non-standard speech.
- **Cognitive and learning:** summarizing, simplifying language, reading aloud, and breaking tasks into steps.
- **Language:** real-time translation for people working in a second language.

**Key example: Be My Eyes "Be My AI."** Be My Eyes connects blind and low-vision people with sighted volunteers by video. In 2023 it added Be My AI, built on OpenAI's GPT-4 vision model: users take a photo and get a detailed spoken description, then ask follow-up questions. In beta, 16,000 users were requesting about 25,000 descriptions a day. It is now also used in Microsoft's Disability Answer Desk and on Windows to describe screens and diagrams.

**Risks and limits:**

- **Errors with no one to catch them:** a blind user may not be able to check a wrong description, so mistakes matter more. Be My Eyes warns AI can be wrong on complex images, charts or spatial layouts, and keeps human volunteers available.
- **Inaccessible AI tools:** research finds blind users face significant barriers using some AI chat interfaces themselves.
- **Privacy:** photos of homes, documents or medicine may contain sensitive information.

**Why it matters.** Accessibility is where AI's benefits are most concrete and personal, and where design mistakes hurt most. Good accessible AI keeps a human fallback, states uncertainty, and is built with disabled users, not just for them.

---

## 10.6 Effects on People

### Critical thinking (Microsoft Research + Carnegie Mellon, CHI 2025)

319 knowledge workers, 936 tasks:

- More confidence in AI → **less critical thinking**
- More confidence in own skills → **more checking**
- Work shifted from doing to **overseeing**: people struggled to evaluate AI outside their expertise, and results were less diverse.

### Emotional reliance (OpenAI + MIT Media Lab, March 2025)

~40 million interactions plus a 28-day trial with 981 people:

- Emotional chats were rare, concentrated in heavy voice users.
- Brief voice use linked to better well-being.
- Heavy daily use linked to more loneliness and dependence (**correlation, not proof**).

### Expanded context from Research Notes

**Over-reliance and critical thinking**

Key study: Microsoft Research and Carnegie Mellon surveyed 319 knowledge workers who use generative AI weekly, covering 936 real tasks (CHI 2025).

- The more confident people were in the AI, the less critical thinking they applied; the more confident they were in their own skills, the more they checked and improved its output.
- Thinking shifted from doing the task to overseeing the AI: verifying information, adapting outputs, and stewarding quality.
- People found it hardest to evaluate AI in areas where they lacked expertise, and AI users produced less diverse results for the same task.

**Design takeaway:** tools should encourage reflection (prompting users to verify, offering critiques, adapting help to the user's skill level) rather than just delivering finished answers.

**Emotional reliance**

Key study: OpenAI and the MIT Media Lab (March 2025) analyzed about 40 million ChatGPT interactions and ran a 28-day trial with 981 participants using text or voice.

- Emotional conversations were rare overall, concentrated in a small group of heavy users, especially of Advanced Voice Mode.
- Brief voice use was linked to better well-being, but heavy daily use was linked to more loneliness and emotional dependence.
- Heavy users were more likely to see ChatGPT as a "friend." The researchers note this is correlation: lonely people may simply use it more.

**Why it matters.** The same features that make AI pleasant (always available, agreeable, personal) can encourage dependence. Responsible design avoids maximizing engagement for its own sake and nudges people toward real-world support when appropriate.

**Example.** A student uses AI to write every essay outline and loses practice planning arguments; another uses it to critique their own outline first and improves faster.

---

## Try it yourself

### Activity 10.1 · Design check

Pick an AI feature you use (autocomplete, an AI Overview, a voice assistant). Score it 0–2 on each Microsoft stage: initially, during interaction, when wrong, over time.

**What to notice / answers:** Write one change that would improve its lowest score.

---

### Activity 10.2 · Think first, then ask (cognitive forcing)

Answer three questions from this guide's test bank yourself first, then ask a chatbot the same questions. Note when you changed your answer and whether the change was right.

**What to notice / answers:** This is the design that cut overreliance most in research.

---

## KEY TAKEAWAYS

- People mostly use AI as an advisor: asking, information, writing.
- Design for the AI being wrong; aim for calibrated, not maximum, trust.
- The more AI acts alone, the more humans need control.

---

## Key terms

| Term | Definition |
|------|------------|
| **Mental model** | A user's understanding of how a system works. |
| **Calibrated trust** | Trusting AI exactly as much as it deserves. |
| **Automation bias** | Over-relying on automated suggestions, even when wrong. |
| **Cognitive forcing** | Design that makes users think before accepting AI output. |
| **Cognitive offloading** | Letting a tool do thinking you would otherwise do. |
| **Affective use** | Using AI for emotional or social purposes. |

### Additional key terms (from Research Notes)

| Term | Definition |
|------|------------|
| **Human-AI interaction (HAI)** | How people and AI systems communicate and work together. |
| **Overreliance** | Accepting AI output without checking. |
| **Explainability** | Helping users understand why the AI produced an output. |
| **Cognitive forcing function** | A design that makes users think before accepting AI output. |
| **Multimodal** | Using several inputs/outputs: text, voice, images, video. |
| **AI agent** | AI that takes actions on the user's behalf. |
| **Accessibility** | Designing so people with disabilities can use a product fully. |

---

## Sources (from Research Notes)

1. Chatterji et al., How People Use ChatGPT (NBER)
2. Duke Fuqua, How do 700 million people use ChatGPT?
3. Amershi et al., Guidelines for Human-AI Interaction (CHI 2019)
4. Microsoft Research, Guidelines for human-AI interaction design
5. Microsoft Research, Guidelines for Human-AI Interaction (publication)
6. Explore AI Ethics, People + AI Guidebook
7. Google Codelabs, Building Trusted AI Products with the PAIR Guidebook
8. Google PAIR, Explainability + Trust chapter (PDF)
9. AAAI-26, Confidence scores and automation bias (PDF)
10. Beyond Explainable AI (arXiv)
11. Koji, AI over-reliance and automation bias (Bucinca et al.)
12. LongtermWiki, Romeo & Conti review of automation bias (AI & Society)
13. Search Engine Land, Pew study on AI summaries
14. Maginative, Be My Eyes releases Be My AI
15. OpenAI GPT-4V system card (Be My Eyes pilot)
16. Be My Eyes, Desktop app on Windows
17. AIPressRoom, Be My AI for Microsoft customers
18. arXiv, Blind and low-vision users and AI tools
19. The Register, Microsoft researchers on AI and critical thinking
20. Campus Technology, Generative AI could inhibit critical thinking
21. Prolific, The impact of GenAI on critical thinking
22. AI Frontiers, A glimpse into the future of AI companions
23. Engadget, OpenAI and MIT studies on loneliness
24. Futura Sciences, Two studies, one pattern
