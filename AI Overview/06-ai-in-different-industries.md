# 06 AI in Different Industries

The same building blocks show up everywhere: computer vision reads scans and inspects products, NLP handles documents and conversations, predictive analytics forecasts demand and failures, and robotics moves goods and people.

---

## Overview: The Adoption Gap

McKinsey's State of AI 2025 (1,993 respondents, 105 countries):

- **88%** of organizations use AI in at least one business function (up from 78%).
- Only about **7%** have scaled it across the whole company.
- **62%** are at least experimenting with AI agents.

**Almost everyone uses AI; almost no one has scaled it.**

### Expanded context from Research Notes

AI has moved from labs into everyday work in every major industry, but most organizations are still early. McKinsey's State of AI 2025 survey (1,993 respondents in 105 countries) found 88% of organizations use AI in at least one business function, up from 78% a year earlier. Only about 7% have scaled it across the whole company, and 62% are at least experimenting with AI agents.

The same building blocks from the earlier topics show up everywhere: computer vision reads scans and inspects products, NLP handles documents and conversations, predictive analytics forecasts demand and failures, and robotics moves goods and people.

---

## 6.1 Healthcare

### What it is

AI helps doctors find disease earlier, speeds up drug discovery, and takes over paperwork so clinicians can spend more time with patients.

### Main applications

| Application | Technology | Example |
|-------------|------------|---------|
| **Medical imaging** | Computer vision (CNNs) | Models trained on labeled X-rays, CT and MRI scans flag possible tumors, fractures or strokes for a radiologist. As of March 2026, 1,163 of 1,524 FDA-authorized AI devices (76%) were for radiology. |
| **Drug discovery** | Deep learning | DeepMind's AlphaFold predicts a protein's 3D shape from its amino-acid sequence. Its database holds 200 million+ structures. Demis Hassabis and John Jumper shared the 2024 Nobel Prize in Chemistry with David Baker — the first Nobel for an AI-enabled breakthrough. |
| **Clinical documentation** | Speech + NLP | "Ambient AI scribes" listen to the visit and draft the note. Microsoft's DAX Copilot is used in 150+ health systems. |
| **Predictive analytics** | ML | Forecasting sepsis, readmission or deterioration risk. |

### Expanded context from Research Notes

**Medical imaging (computer vision):** Models trained on thousands of labeled X-rays, CT and MRI scans flag possible tumors, fractures or strokes for a radiologist to check. Radiology is by far the biggest area: as of March 2026, 1,163 of the FDA's 1,524 authorized AI medical devices (76%) were for radiology.

**Drug discovery (deep learning):** Google DeepMind's AlphaFold predicts a protein's 3D shape from its amino-acid sequence, work that used to take years of lab experiments. Its database holds over 200 million predicted structures, and its creators Demis Hassabis and John Jumper shared the 2024 Nobel Prize in Chemistry with David Baker, the first Nobel for an AI-enabled breakthrough.

**Clinical documentation (speech + NLP):** "Ambient AI scribes" listen to the doctor-patient conversation and draft the medical note. Microsoft's DAX Copilot is used in 150+ health systems.

**Predictive analytics:** Forecasting which patients are at risk of sepsis, readmission or deterioration so staff can act sooner.

### Why it matters

Doctors are short on time and many regions lack specialists. AI can triage urgent scans, reduce burnout from paperwork, and cut years off early drug research, where most drug candidates fail.

### Example

A hospital's AI flags a CT scan showing a likely brain bleed and moves it to the top of the radiologist's queue, so the patient is seen minutes instead of hours later.

### Challenges

- Patient privacy
- Bias when training data underrepresents some groups
- Unclear responsibility when AI is wrong
- A gap between strong test results and proven benefit in real hospitals

### Sources (from Research Notes)

- Radiology Business, FDA AI list: 1,524 algorithms, 1,163 for radiology
- FDA, List of AI-Enabled Medical Devices
- Drug Target Review, Nobel Prize celebrates AI's role in protein structure
- Deepgram, Top medical AI models 2026

---

## 6.2 Education

### What it is

AI in education means tools that tutor students one-on-one, adapt lessons to each learner, and save teachers time on planning and grading.

### Main applications

- **AI tutors (LLMs):** guide step by step with hints instead of answers (Khan Academy's Khanmigo).
- **Adaptive learning (predictive analytics):** chooses the next exercise at the right difficulty. China's Squirrel AI reports 24 million+ registered students.
- **Teacher tools:** lesson plans, quizzes, rubrics, feedback.
- **Accessibility:** speech-to-text, translation, reading support.

### Expanded context from Research Notes

**AI tutors (LLMs):** Chatbots that guide students step by step with hints and questions instead of giving the answer, like Khan Academy's Khanmigo.

**Adaptive learning (predictive analytics):** Platforms track which questions a student gets right or wrong and choose the next exercise at the right difficulty. China's Squirrel AI says it has more than 24 million registered students.

**Teacher tools:** Drafting lesson plans, quizzes, rubrics and feedback on essays.

**Accessibility:** Speech-to-text, translation and reading support for students with disabilities or learning in a second language.

### Evidence

A 2025 Harvard randomized trial with 194 physics students found those using a carefully designed AI tutor learned **more than twice as much** as in an active-learning class, in less time (median ~49 min vs a 60-min class), and felt more engaged. It worked because it made students **reason step by step** (short replies), not because it handed out answers.

### The catch

**Access ≠ use.** Only ~15% of students with Khanmigo access use it regularly; a Stanford study found AI tutor use of only **2–5 minutes a week**.

### Expanded context from Research Notes

The Harvard tutor worked because it was designed to make students reason (short replies, step-by-step guidance), not to hand out answers.

### Example

Before class, students work through a new topic with an AI tutor at home; the teacher reads AI summaries of where students got stuck and uses class time on those points.

### Challenges

- Cheating and over-reliance
- Wrong answers from the AI
- Student data privacy
- Unequal access to devices and internet

### Sources (from Research Notes)

- Kestin et al., AI Tutoring Outperforms Active Learning (Harvard)
- Hechinger Report on the Harvard AI tutor study
- EdTech Innovation Hub, Only 15% of students with Khanmigo access use it
- Let's Data Science, AI tutors and the Stanford engagement study
- DEV Community, Twice the Learning, Half the Wisdom (Squirrel AI)

---

## 6.3 Business

### What it is

Businesses use AI to serve customers, sell and market, manage money and risk, and speed up everyday office work. It is the most widespread area: in McKinsey's 2025 survey half of organizations use AI in three or more business functions, led by IT, knowledge management, marketing and sales.

### Main applications

| Area | Technology | Example |
|------|------------|---------|
| **Customer service** | NLP + LLMs | 24/7 chatbots that hand complex cases to humans. |
| **Marketing and sales** | Generative AI + predictive analytics | Ad copy, personalized recommendations, lead scoring. |
| **Finance** | Classification | Fraud detection, credit scoring, spotting unusual transactions in real time. |
| **Operations** | LLMs, agents | Meeting summaries, reports, code, AI agents that carry out multi-step tasks. |

### Expanded context from Research Notes

**Customer service (NLP + LLMs):** Chatbots answer common questions 24/7 in many languages and hand complex cases to humans.

**Marketing and sales (generative AI + predictive analytics):** Writing ad copy and emails, personalizing product recommendations, scoring which leads are most likely to buy.

**Finance and banking (classification):** Fraud detection, credit scoring and spotting unusual transactions in real time.

**Operations and productivity:** Summarizing meetings and documents, drafting reports, writing code, and "AI agents" that carry out multi-step tasks.

### Why it matters

AI lets companies handle much more work without hiring at the same rate, and respond to customers instantly.

### Klarna case study

Its OpenAI-powered assistant handled **2.3 million chats in its first month** (Feb 2024), two-thirds of all chats, the work of ~700 full-time agents. Satisfaction matched humans, resolution time fell from **11 minutes to under 2**, and repeat questions fell **25%**.

Klarna later moved to a **hybrid model**, promising customers can always reach a real person.

### Challenges

- Stuck in pilots (only about 7% have scaled AI companywide)
- Chatbot frustration on complex problems
- Wrong content
- Job impacts on roles like customer support

### Sources (from Research Notes)

- Chain Store Age, Klarna AI assistant results
- PromptLayer, Klarna from AI-first to human-hybrid
- Neodata, McKinsey State of AI 2025 summary
- GRC Report, McKinsey 2025 findings

---

## 6.4 Manufacturing ("Industry 4.0")

### What it is

Factories use AI to keep machines running, catch defects, and automate production with smarter robots. This is often called "Industry 4.0" or the smart factory.

### Main applications

| Application | Technology | Example |
|-------------|------------|---------|
| **Predictive maintenance** | Predictive analytics + sensors | Sensors record vibration, temperature and sound; a model spots patterns before breakdowns. McKinsey: up to 50% less downtime and 10–40% lower maintenance costs. Deloitte: poor maintenance can cut capacity by 5–20%. |
| **Visual quality inspection** | Computer vision | Cameras and deep learning spot scratches, cracks or missing parts. BMW AIQX spots assembly errors; at Dingolfing it tells real defects from dust or oil. Foxconn's system runs 40× faster than before on NVIDIA hardware. |
| **Industrial robots** | Robotics | 5 million in factories (2025); China installed 354,000 (59%). |
| **Digital twins** | Simulation + AI | Virtual copies of factories for testing changes in simulation and optimizing schedules and supply chains. |

### Expanded context from Research Notes

**Predictive maintenance (predictive analytics + sensors):** Sensors on machines record vibration, temperature and sound; a model learns the patterns that come before a breakdown and alerts staff to fix the part in advance.

**Visual quality inspection (computer vision):** Cameras on the production line photograph every part, and a deep learning model spots scratches, cracks or missing pieces faster and more consistently than tired human eyes.

**Industrial robots:** The IFR's World Robotics 2026 report counts a record 5 million industrial robots working in factories in 2025, with China installing 354,000 that year (59% of the world total).

**Digital twins and planning:** Virtual copies of a factory let engineers test changes in simulation and AI optimize schedules and supply chains.

### Why it matters

Unplanned downtime is very expensive, and Deloitte estimates poor maintenance can cut a plant's productive capacity by 5–20%. AI helps factories produce more, waste less, and keep quality consistent around the clock.

### Examples

- **BMW:** its AIQX ("Artificial Intelligence Quality Next") system uses cameras along the line to spot assembly errors; at the Dingolfing plant, AI tells real defects on metal parts apart from harmless dust or oil drops.
- **Foxconn:** built an AI inspection system for surface defects on electronics components, running on NVIDIA hardware over 40× faster than its earlier setup.

### Challenges

- High setup cost
- Messy or missing sensor data
- A shortage of workers with both factory and AI skills
- Cybersecurity risks
- Worries about job losses

### Sources (from Research Notes)

- Körber, AI-driven predictive maintenance (McKinsey figures)
- Tesseract Academy, Predictive maintenance benefits (Deloitte figures)
- Australian Manufacturing, IFR World Robotics 2026
- Analytics Insight, How BMW uses AI to detect defects
- NVIDIA, Foxconn on AI in industrial manufacturing

---

## 6.5 Transportation

### What it is

AI is changing how people and goods move: self-driving vehicles, smarter delivery routes, and traffic and fleet management.

### Main applications

- **Robotaxis** (computer vision + robotics)
- **Route optimization** (optimization + predictive analytics)
- **Driver assistance** (lane keeping, automatic emergency braking)
- **Fleet and traffic management**

### Expanded context from Research Notes

**Self-driving cars and robotaxis (computer vision + robotics):** Cameras, lidar and radar feed models that detect cars, people and signs, predict what they'll do next, and plan a safe path (see the Robotics section of the ML notes).

**Route optimization (optimization + predictive analytics):** Algorithms find the shortest delivery order across many stops, updated with live traffic.

**Driver assistance:** Lane keeping, automatic emergency braking and adaptive cruise control in ordinary cars.

**Fleet and traffic management:** Predicting vehicle maintenance, demand for rides, and adjusting traffic signals.

### Why it matters

Most road crashes involve human error, delivery networks burn huge amounts of fuel, and many regions face driver shortages. Even small efficiency gains add up across millions of trips.

### Key examples

- **Waymo (USA):** giving about 500,000 paid driverless rides per week by March 2026, with a target of 1 million per week by the end of 2026.
- **Baidu Apollo Go (China):** operates robotaxis across more than 3,000 km² of Wuhan and other cities, and launched full commercial service in Dubai in April 2026.
- **UPS ORION:** route-optimization software used by 55,000 US drivers saves about 100 million miles and 10 million gallons of fuel a year, worth an estimated $300–400 million annually. UPS says cutting just one mile per driver per day saves up to $50 million a year.

### Challenges

- Safety in rare, unexpected situations
- System-wide failures (in early April 2026, a mass Apollo Go malfunction in Wuhan stranded passengers and halted traffic)
- Unclear legal responsibility after crashes
- Public trust
- Effects on drivers' jobs

### Sources (from Research Notes)

- Bloomberg, Waymo co-CEO on 1 million weekly trips
- ai2.work, Waymo hits 500,000 weekly rides
- It Can Think, Baidu and the global competition for robotaxis
- eWeek, Baidu robotaxi failure strands riders in Wuhan
- INFORMS, UPS ORION project
- Best Practice AI, UPS ORION case study

---

## Comparison

| Field | Key technology | Standout example | Biggest challenge |
|-------|----------------|------------------|-------------------|
| **Healthcare** | Vision, deep learning, NLP | AlphaFold (2024 Nobel) | Privacy, bias, real-world proof |
| **Education** | LLMs, predictive analytics | Harvard tutor: 2× gains | Low uptake, cheating |
| **Business** | NLP, LLMs, classification | Klarna: work of ~700 agents | Scaling beyond pilots |
| **Manufacturing** | Sensors + ML, vision, robotics | BMW AIQX | Cost, data, skills |
| **Transportation** | Vision, robotics, optimization | Waymo ~500K rides/week | Safety, liability, trust |

### Expanded context from Research Notes

| Field | Main AI uses | Key technology | Standout example | Biggest challenge |
|-------|--------------|----------------|------------------|-------------------|
| **Healthcare** | Scan reading, drug discovery, clinical notes | Computer vision, deep learning, NLP | AlphaFold (2024 Nobel Prize) | Privacy, bias, real-world proof |
| **Education** | AI tutors, adaptive learning, teacher tools | LLMs, predictive analytics | Harvard AI tutor: 2× learning gains | Low student uptake, cheating |
| **Business** | Customer service, marketing, fraud detection | NLP, LLMs, classification | Klarna bot: work of ~700 agents | Scaling beyond pilots |
| **Manufacturing** | Predictive maintenance, inspection, robots | Sensors + ML, computer vision, robotics | BMW AIQX quality inspection | Cost, data, skills |
| **Transportation** | Robotaxis, route optimization, driver assist | Computer vision, robotics, optimization | Waymo: ~500,000 rides/week | Safety, liability, trust |

---

## Try it yourself

### Activity 6.1 · Principal's decision (scenario)

You run a school deciding whether to adopt an AI tutor. Using the Harvard study and the Khanmigo uptake numbers, list 2 benefits, 2 risks and 1 way to make students actually use it.

**What to notice / answers:** Strong answers mention design (step-by-step hints, not answers) and the gap between access and use.

---

### Activity 6.2 · Match the example (paper)

Match each example to its industry and main technology: AlphaFold, Klarna assistant, BMW AIQX, UPS ORION, ambient AI scribe, Waymo.

**Answers:**
- AlphaFold → Healthcare / deep learning
- Klarna assistant → Business / LLM + NLP
- BMW AIQX → Manufacturing / computer vision
- UPS ORION → Transportation / route optimization
- Ambient AI scribe → Healthcare / speech + NLP
- Waymo → Transportation / vision + robotics

---

## KEY TAKEAWAYS

- 88% use AI, 7% have scaled it.
- Design decides results (Harvard tutor), humans stay in the loop (Klarna hybrid), and failures scale too (Wuhan outage).

---

## Key terms

| Term | Definition |
|------|------------|
| **Scaling** | Rolling AI out across the whole organization, beyond pilots. |
| **Predictive maintenance** | Fixing machines before they fail, based on sensor patterns. |
| **Ambient AI scribe** | AI that listens to a doctor visit and drafts the note. |
| **Adaptive learning** | Choosing each student's next exercise by their performance. |
| **Digital twin** | A virtual copy of a factory or system for simulation. |

---

## Complete Sources List (from Research Notes)

1. McKinsey, AI at work but not at scale (State of AI 2025)
2. Radiology Business, FDA AI device list breakdown
3. FDA, List of AI-Enabled Medical Devices
4. Drug Target Review, Nobel Prize and AlphaFold
5. Deepgram, Top medical AI models 2026
6. Kestin et al., AI Tutoring Outperforms Active Learning
7. EdTech Innovation Hub, Khanmigo usage
8. Chain Store Age, Klarna AI assistant results
9. Körber, AI predictive maintenance
10. Australian Manufacturing, IFR World Robotics 2026
11. Analytics Insight, BMW AI defect detection
12. Bloomberg, Waymo 1 million weekly trips target
13. eWeek, Apollo Go outage in Wuhan
14. INFORMS, UPS ORION
