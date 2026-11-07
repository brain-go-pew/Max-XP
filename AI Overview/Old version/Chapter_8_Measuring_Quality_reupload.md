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
