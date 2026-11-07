# 11 AI Ethics & Social Responsibility

How AI should be built and used so it benefits people and avoids harm: who it helps, who it might hurt, and who is responsible when something goes wrong.

---

## 11.1 The Global Baseline

In November 2021, all **193 UNESCO member states** adopted the Recommendation on the Ethics of AI, the first global standard. It isn't legally binding, but countries report on how they apply it. It has 10 core principles and actions in 11 policy areas.

### Core principles

| Principle | Plain meaning |
|-----------|---------------|
| **Fairness / non-discrimination** | No unfair treatment of groups |
| **Transparency / explainability** | People know when AI is used and roughly how it decides |
| **Privacy / data protection** | Personal data used lawfully and minimally |
| **Safety / security** | Works reliably and resists misuse |
| **Accountability** | A human or organization stays responsible |
| **Human oversight** | People can review, override or appeal |
| **Sustainability** | Energy, water and environmental costs |

### The challenge

Principles are easy to agree on and hard to apply.

### Expanded context from Research Notes

AI ethics asks how AI should be built and used so it benefits people and avoids harm: who it helps, who it might hurt, and who is responsible when something goes wrong. Social responsibility extends this to companies, governments and users.

**The global baseline.** In November 2021, all 193 UNESCO member states adopted the Recommendation on the Ethics of Artificial Intelligence, the first global standard on AI ethics. It isn't legally binding, but countries agreed to report on how they put it into practice. It is built on ten core principles and gives concrete actions in eleven policy areas, including health, the environment and gender.

**Principles that appear in almost every framework** (UNESCO, OECD, EU, company policies):

| Principle | Plain meaning |
|-----------|---------------|
| **Fairness / non-discrimination** | AI shouldn't treat groups of people unfairly |
| **Transparency and explainability** | People should know when AI is used and roughly how it decides |
| **Privacy and data protection** | Personal data is collected and used lawfully and minimally |
| **Safety and security** | AI should work reliably and resist misuse |
| **Accountability** | A human or organization stays responsible for outcomes |
| **Human oversight** | People can review, override or appeal AI decisions |
| **Sustainability** | Consider energy, water and environmental costs |

**Why it matters.** Principles are easy to agree on but hard to apply. The rest of these notes look at where they're tested in practice: bias, misinformation, privacy, laws and accountability.

---

## 11.2 Bias and Fairness

### Cases

- **Gender Shades** (34.7% vs 0.8% errors) — see Topic 9.
- **Amazon hiring** (downgraded "women's") — see Topic 9.

### Ethical questions

1. **Whose data?** Who was left out, and who decided?
2. **Which fairness?** Equal accuracy, equal approval rates, or equal error rates? They can conflict, so choosing is a value judgment.
3. **Should AI be used here at all?** Predicting crime or emotions from faces may be too risky regardless of accuracy.

### Responses

- Per-group testing
- Representative data
- Independent bias audits (NYC Local Law 144 requires them for AI hiring tools)
- Treating hiring, credit and education AI as **high-risk** (EU AI Act)

### Expanded context from Research Notes

**What it is.** Algorithmic bias is when an AI system produces systematically worse or unfair outcomes for certain groups, often by race, gender, age, disability or language. (The Failure Modes notes cover how bias happens technically.)

**Well-known cases:**

- **Face analysis (Gender Shades, 2018):** commercial systems misclassified darker-skinned women up to 34.7% of the time vs. at most 0.8% for lighter-skinned men.
- **Hiring (Amazon, 2018):** a resume-screening AI trained mostly on men's resumes learned to downgrade resumes mentioning "women's"; the project was scrapped.

**Ethical questions it raises:**

- **Whose data?** Who was left out of the training data, and who decided?
- **Which fairness?** Equal accuracy for all groups, equal approval rates, or equal error rates? These definitions can conflict, so choosing one is a value judgment, not just a technical choice.
- **Should AI be used here at all?** Some uses, like predicting crime or emotions from faces, may be too risky regardless of accuracy.

**Responses:** testing performance separately for each group, more representative data, independent bias audits (New York City requires them for AI hiring tools under Local Law 144), and laws treating hiring, credit and education AI as "high-risk" (EU AI Act).

**Why it matters.** Biased AI can scale discrimination to millions of decisions while appearing objective, and those affected often never learn an AI was involved.

---

## 11.3 Misinformation and Deepfakes

### Three harms

1. **Fraud and scams** (impersonating faces and voices)
2. **Misinformation** (fake news, election manipulation, AI errors spread as fact)
3. **Personal abuse** (non-consensual intimate images, harassment)

### The Arup case (2024)

A finance employee in Arup's Hong Kong office joined a video call with what looked like the UK CFO and colleagues. Everyone else was a **deepfake** built from public video and audio. He made 15 transfers totaling **HK$200 million (~US$25.6 million)** to five accounts, discovered only when he checked with head office.

### Labeling

- **China:** requires visible labels + hidden metadata (since Sept 2025).
- **EU AI Act:** Article 50 transparency rules (since Aug 2026).

### Targeted laws

- **US TAKE IT DOWN Act** (May 2025) criminalizes sharing non-consensual intimate deepfakes.
- **EU** bans on "nudifier" apps and AI child abuse material.

### Defense habits

- Call back on a known number.
- Use code words.
- Two-person payment approval.

### The "liar's dividend"

When anything can be faked, people may stop trusting real evidence too.

### Expanded context from Research Notes

Generative AI makes it cheap and fast to create convincing fake text, images, audio and video (deepfakes). The harm comes in three forms:

- **Fraud and scams:** impersonating real people's faces and voices.
- **Misinformation:** false news, fake evidence, election manipulation; also accidental errors from AI tools spreading as fact (see the Accuracy notes).
- **Personal abuse:** fake intimate images made without consent, harassment and reputational attacks.

**Key example: Arup deepfake scam (2024).** A finance employee at engineering firm Arup's Hong Kong office joined a video call with what looked and sounded like the company's UK CFO and other colleagues. Every other person on the call was an AI deepfake built from public video and audio. Convinced, the employee made 15 transfers totaling HK$200 million (about US$25.6 million) to five bank accounts. The fraud was discovered only when he later checked with head office.

**Responses:**

- **Labeling and watermarking:** China requires both visible labels and hidden metadata on AI-generated content (since September 2025); the EU AI Act's transparency rules (Article 50) require disclosing AI interactions and marking AI-generated content (since August 2026).
- **Targeted laws:** the US TAKE IT DOWN Act (May 2025) criminalizes sharing non-consensual intimate deepfakes; the EU added bans on "nudifier" apps and AI-generated child abuse material.
- **Verification habits:** call back on a known number, use code words, require two people to approve payments.

**Why it matters.** When anything can be faked, people may stop trusting real evidence too (sometimes called the "liar's dividend"). Protecting trust in information is a shared job for companies, governments and users.

---

## 11.4 Privacy, Data and Copyright

### Privacy concerns

- Personal data in training sets without consent
- Users sharing sensitive details
- Models revealing personal data
- Difficulty deleting data from a trained model
- Age checks

### Italy fines OpenAI (Dec 2024)

Italy's Garante (which briefly banned ChatGPT in 2023) fined OpenAI **€15 million** under GDPR:

- Training on personal data without legal basis
- Transparency failures
- An unreported March 2023 breach
- Weak age checks

Ordered a six-month public campaign. OpenAI said it would appeal.

### Bartz v. Anthropic

Authors sued over millions of pirated books used to train Claude. In June 2025 Judge William Alsup ruled:

- Training on **lawfully obtained** books was fair use.
- Building a library from **pirate sites** was not.

**Settlement:** $1.5 billion (~$3,000 per book, ~500,000 books), pirated files destroyed; final approval July 2026 — the largest copyright recovery in US history.

### Expanded context from Research Notes

AI models are trained on enormous amounts of data, often scraped from the internet, and chatbots collect what users type. This raises two big questions: was the data used lawfully and fairly, and what happens to what users share?

**Privacy concerns:**

- Personal information in training data (names, posts, photos) used without consent.
- Users sharing sensitive details (health, work secrets) in chats.
- Models that can repeat or reveal personal data, and the difficulty of deleting someone's data from a trained model.
- Age checks and protecting children.

**Example: Italy fines OpenAI (December 2024).** Italy's data protection authority (Garante), which had briefly banned ChatGPT in 2023, fined OpenAI €15 million under the EU's GDPR. It found OpenAI had used personal data to train ChatGPT without an adequate legal basis, didn't meet transparency duties, failed to report a March 2023 data breach, and lacked proper age verification. OpenAI was also ordered to run a six-month public information campaign. OpenAI called the fine disproportionate and said it would appeal.

**Copyright concerns.** Writers, artists, musicians and news outlets argue AI companies trained on their work without permission or payment. Dozens of lawsuits are ongoing.

**Example: Bartz v. Anthropic.** Authors sued Anthropic for downloading millions of pirated books to train its Claude models. In June 2025, Judge William Alsup ruled that training AI on lawfully obtained books was fair use, but that building a library from pirate sites was not. Anthropic settled for $1.5 billion (about $3,000 per book for nearly 500,000 books) and agreed to destroy the pirated files. A judge gave final approval in July 2026; it is described as the largest copyright recovery in US history.

**Why it matters.** These cases are setting the rules for how AI can be built. Users should also be careful about what they share with AI tools and check privacy settings.

---

## 11.5 Regulation Around the World (as of November 2026)

| Region | Approach | Key rules and status |
|--------|----------|---------------------|
| **EU** | One comprehensive, risk-based law (AI Act) | In force Aug 2024. Bans since Feb 2025; general-purpose AI rules Aug 2025; transparency (Art. 50) Aug 2026. The 2026 "Digital Omnibus" delayed high-risk rules to Dec 2027 (Aug 2028 for regulated products) and added bans on nudifier apps and AI child abuse material. |
| **China** | Targeted rules from the Cyberspace Administration of China | 2023 Interim Measures for Generative AI; deep synthesis rules (2023); mandatory labels with hidden metadata (Sept 2025); no single national AI law. |
| **US** | No federal AI law; executive orders + state laws | Dec 2025 executive order seeks a national framework and challenges state laws, but nothing preempts them. State laws: California SB 53 (frontier AI transparency, Jan 2026), Texas TRAIGA; Colorado replaced its 2024 Act with a narrower law from 2027. Dispute unresolved. |
| **Global** | Voluntary principles | UNESCO Recommendation (2021); OECD AI Principles. |

### EU AI Act risk tiers

| Tier | Description | Examples |
|------|-------------|----------|
| **1. Unacceptable — banned** | Government social scoring, manipulative AI exploiting vulnerable people | |
| **2. High — strict rules** | Hiring, credit, education, law enforcement, border control, critical infrastructure (risk management, data quality, human oversight, documentation) | |
| **3. Limited — transparency** | Chatbots must say they're AI; AI content must be marked | |
| **4. Minimal — no new duties** | Spam filters, video games | |

### The debate

Supporters say rules protect rights and trust; critics say strict or fragmented rules raise costs and slow innovation. The EU's own delay shows how hard it is.

### Expanded context from Research Notes

Countries are taking different approaches: the EU uses one broad risk-based law, China uses targeted rules from its internet regulator, and the US has no single federal AI law, relying on executive orders and state laws. (Status as of November 2026.)

| Region | Main approach | Key rules and status |
|--------|---------------|---------------------|
| **European Union** | One comprehensive, risk-based law (EU AI Act) | In force since August 2024. Bans on "unacceptable risk" uses since February 2025; general-purpose AI rules since August 2025; transparency rules (Article 50) since August 2026. The 2026 "Digital Omnibus" delayed high-risk rules (hiring, credit, education, law enforcement) to December 2027, and to August 2028 for AI in regulated products, while adding new bans on nudifier apps and AI child abuse material |
| **China** | Targeted regulations led by the Cyberspace Administration of China | 2023 Interim Measures for Generative AI Services; deep synthesis rules (2023); mandatory AI content labeling with visible labels plus hidden metadata (since September 2025); no single national AI law yet |
| **United States** | No comprehensive federal AI law; executive orders plus state laws | A December 2025 executive order seeks a national framework and directs challenges to state AI laws, but no federal law preempts them. State laws in effect include California SB 53 (frontier AI transparency, since January 2026) and Texas TRAIGA; Colorado replaced its 2024 AI Act with a narrower law starting 2027. The federal-state dispute is unresolved |

**EU AI Act risk tiers:**

1. **Unacceptable risk → banned:** e.g., social scoring by governments, manipulative AI that exploits vulnerable people.
2. **High risk → strict rules:** AI used in hiring, credit, education, law enforcement, border control, critical infrastructure; requires risk management, data quality, human oversight and documentation.
3. **Limited risk → transparency:** chatbots must say they're AI; AI-generated content must be marked.
4. **Minimal risk → no new duties:** e.g., spam filters, AI in video games.

**The debate.** Supporters of stronger rules argue they protect rights and build public trust. Critics argue strict or fragmented rules raise costs and slow innovation. The EU's own delay of high-risk rules, citing late technical standards, shows how hard it is to regulate a fast-moving technology.

---

## 11.6 Responsibility and Accountability

AI can't be held accountable itself, so responsibility sits with **people and organizations**.

### The four actors and their duties

| Actor | Duty |
|-------|------|
| **Developers** | Safe design, testing, documenting limits |
| **Deployers** | Appropriate use, human oversight, informing people |
| **Governments** | Laws, enforcement, public education |
| **Users** | Checking outputs, not misusing tools, disclosing AI use |

### Transparency

2024) to 40 (2025). IBM scored highest ever (95); Meta fell 60 → 31; Mistral 55 → 18. Least disclosed: training data and compute.

### Courts

Courts hold lawyers, not ChatGPT, responsible for fake citations: **"the AI did it" is not a defense.**

### Expanded context from Research Notes

When AI causes harm (a wrong medical suggestion, a biased rejection, a robotaxi crash, a fake citation in court), who is responsible? AI can't be held accountable itself, so responsibility has to sit with people and organizations.

**Who carries responsibility:**

| Actor | Responsibilities |
|-------|------------------|
| **Developers (AI companies)** | Safe design, testing, documenting risks and limits, preventing misuse |
| **Deployers (organizations using AI)** | Appropriate use, human oversight, informing people |
| **Governments** | Laws, enforcement, public education |
| **Users** | Checking outputs, not misusing tools, disclosing AI use |

**Common accountability tools:** model cards and system cards (documenting what a model can and can't do), red-teaming (attacking your own system to find risks), impact assessments, independent audits, incident reporting, and human review for high-stakes decisions.

**Transparency is slipping.** Stanford's 2025 Foundation Model Transparency Index scored major AI developers on 100 disclosure indicators. The average fell from 58 out of 100 in 2024 to 40 in 2025. IBM scored highest ever at 95; Meta dropped from 60 to 31 and Mistral from 55 to 18. Companies were least open about training data and compute. Without disclosure, outsiders can't check claims about safety or fairness.

**Example.** Courts have made clear that lawyers, not ChatGPT, are responsible for fake citations in their filings, and have fined them (see the Accuracy notes). The same principle applies widely: "the AI did it" is not a defense.

**Why it matters.** Social responsibility means thinking beyond what's legal: who might be harmed, who is left out, and what happens to jobs, the environment and public trust.

---

## Try it yourself

### Activity 11.1 · Sort by EU AI Act risk tier (paper)

Place each in a tier: government social scoring, a CV-screening tool, a customer service chatbot, a spam filter, an AI exam-proctoring system, a video-game character.

**Answers:**
- Government social scoring → **Unacceptable**
- CV-screening tool → **High**
- Customer service chatbot → **Limited**
- Spam filter → **Minimal**
- AI exam-proctoring system → **High** (education)
- Video-game character → **Minimal**

---

### Activity 11.2 · Deepfake defense plan (scenario)

You get a video call from your company's "CFO" asking for an urgent transfer. Write three things you would do before sending any money.

**What to notice / answers:** E.g. call back on a known number, use a code word, require a second person to approve (the Arup lessons).

---

## KEY TAKEAWAYS

- UNESCO's principles are shared worldwide but hard to apply ("which fairness?").
- Three landmark cases: Arup (deepfake fraud), Italy (privacy), Bartz (copyright).
- EU = one risk-based law; China = targeted rules; US = no federal law.

---

## Key terms

| Term | Definition |
|------|------------|
| **Deepfake** | AI-generated fake video, image or audio of a real person. |
| **Watermarking** | Marking content as AI-generated, visibly or in metadata. |
| **GDPR** | The EU's data protection law. |
| **Fair use** | US doctrine allowing some uses of copyrighted work without permission. |
| **Preemption** | A federal law overriding state laws. |
| **Model card** | Documentation of a model's purpose, limits and risks. |
| **Red-teaming** | Deliberately attacking a system to find weaknesses. |

### Additional key terms (from Research Notes)

| Term | Definition |
|------|------------|
| **AI ethics** | Principles for building and using AI to benefit people and avoid harm. |
| **Algorithmic bias** | Systematically unfair results for certain groups. |

---

## Sources (from Research Notes)

1. UNESCO Netherlands, The UNESCO Recommendation on the Ethics of AI (brochure)
2. AlgorithmWatch, UNESCO adopts Recommendation on the Ethics of AI
3. Regulations.ai, UNESCO AI Ethics Recommendation summary
4. Buolamwini & Gebru, Gender Shades (PMLR)
5. MIT Technology Review, Amazon ditched AI recruitment software
6. MMOww, AI Compliance: United States 2026 (NYC Local Law 144)
7. CNN via ABC17, Arup revealed as $25 million deepfake scam victim
8. Business Insider NL, Arup deepfake scam details
9. CMS, China releases AI content labeling rules
10. Orrick, EU Digital Omnibus changes (new bans)
11. MMOww, AI Compliance: United States 2026 (TAKE IT DOWN Act)
12. Analytics India Magazine, Italy fines OpenAI €15 million
13. JD Supra / Sheppard Mullin, Italy's first GenAI GDPR fine
14. Jurist, Judge approves record $1.5 billion Anthropic settlement
15. Association of American Publishers, Final approval in Bartz v. Anthropic
16. The Next Web, Anthropic settlement approved
17. Orrick, EU AI Act Digital Omnibus finalizes 8 changes
18. AI Act Explorer, Digital Omnibus on AI
19. The Agent Index, EU AI Act timeline after the Digital Omnibus
20. CASRAI, China's AI regulation explained
21. Loeb & Loeb, China's AI labeling measures
22. GLACIS, US state AI laws tracker
23. CASRAI, Federal AI preemption fight: where it stands
24. Inside Deep Tech, AI safety laws in the US: 2026 update
25. Stanford HAI, Transparency in AI is on the decline
26. Bommasani et al., The 2025 Foundation Model Transparency Index (arXiv)
27. Stanford Report, AI companies average 40/100 on transparency
28. Bloomberg Law, AI faked cases irritate judges
