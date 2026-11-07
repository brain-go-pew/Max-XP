# 03 Machine Learning & Deep Learning

Machine learning is the core idea behind every AI system in this guide. Everything else is a way of learning (supervised, unsupervised, reinforcement), a type of model (deep neural networks), or a place ML is applied (prediction, vision, robots).

---

## How this fits together (from Research Notes)

Machine learning (ML) is the core idea; every other section is either a way of learning (supervised, unsupervised, reinforcement), a type of model (deep neural networks), or a place where ML is applied (language, prediction, vision, robots).

Each topic below follows the same pattern: What it is, How it works, Why it matters, Example, and Sources. Sources are listed per section and collected again at the end.

---

## 3.1 Introduction to Machine Learning

### What it is

A branch of AI where computers learn patterns from data instead of following rules a programmer writes by hand. The term comes from IBM researcher Arthur Samuel, whose 1959 paper described a checkers program that got better the more it played. It played thousands of games against itself and beat a strong human player in 1962.

### Traditional programming vs machine learning

| Traditional programming | Machine learning |
|------------------------|------------------|
| Rules + data → answers | Data + answers → rules |

### The training loop

1. **Collect data:** examples of the problem.
2. **Pick a model:** a math function with adjustable settings called parameters.
3. **Train:** the model makes predictions, a loss function scores how wrong they are, and an optimizer nudges the parameters to reduce the error. Repeat thousands of times.
4. **Test** on data the model has never seen, to check it learned the pattern rather than memorizing it (overfitting).
5. **Deploy and monitor,** because real-world data drifts over time.

### Why it matters

ML powers search ranking, recommendations, spam filters, translation and chatbots.

- Stanford's 2026 AI Index: generative AI reached **53% adoption within three years**, faster than the PC or the internet.
- US private AI investment was about **$286 billion in 2025**.

### Example (from Research Notes)

Samuel's checkers program played thousands of games against itself and used the results to improve its board scoring, eventually beating a strong human player in 1962.

### Where ML fits

- **Artificial intelligence (AI):** the broad goal of machines doing tasks that need human-like intelligence.
- **Machine learning (ML):** the main way to get there today (learning from data).
- **Deep learning:** ML with many-layered neural networks (3.5).
- **Generative AI:** deep learning that creates new content (Topic 4).

Every system in use today is **narrow AI**: good at specific tasks. **Artificial general intelligence (AGI)** — AI as capable as people across almost all tasks — does not exist yet and its timing is debated.

### Parameters vs hyperparameters

| Parameters | Hyperparameters |
|------------|----------------|
| Learned by the model during training (weights, biases) | Chosen by people before training (learning rate, number of layers, k in k-means, tree depth) |
| Example: the w and b in y = w·x + b | Tuned by trying values and checking the validation set |

### Data comes first

Most of the work in real ML projects is **collecting, cleaning and labeling data**: fixing missing values, removing duplicates, and checking the data represents everyone the model will be used on. Bad data creates bad and biased models (Topic 9).

### Key terms (from Research Notes)

- **Dataset:** the collection of examples used for training and testing.
- **Feature:** an input variable (e.g., house size).
- **Label:** the right answer in training data.
- **Model:** the math function with adjustable parameters.
- **Training:** the process of adjusting parameters to reduce error.
- **Overfitting:** memorizing training data instead of learning the general pattern.

### Sources (from Research Notes)

- Forbes via AITopics: Samuel and the origin of "machine learning"
- AITopics: Samuel's checkers win
- Stanford HAI, 2026 AI Index Report

---

## 3.2 Supervised Learning

### What it is

The model learns from **labeled examples**: each input (features) comes with the correct answer (label). After training, it predicts labels for new inputs. Supervised learning splits into two tasks based on the kind of answer.

### Classification vs regression

| | Classification | Regression |
|---|---|---|
| **Predicts** | A category (spam / not spam) | A number (price, temperature) |
| **Algorithms** | Logistic regression, decision trees, random forest, SVM, neural networks | Linear regression, decision trees, gradient boosting, neural networks |
| **Scored by** | Accuracy, precision, recall, F1 | MAE, MSE, R² |
| **Example** | Spam filter, diagnosis from scans | House-price estimate, sales forecast |

### How it works

The algorithm looks at many labeled examples and adjusts itself to minimize **loss**, the penalty for wrong predictions. Data is split into:

- **Training set** (to learn)
- **Validation set** (to tune)
- **Test set** (to check final performance)

### Classification details

The model outputs a probability for each class; a threshold turns it into a decision ("spam if probability > 0.5"). Results go in a **confusion matrix** (true/false positives and negatives):

- **Precision** = of the emails flagged as spam, how many really were?
- **Recall** = of all real spam, how much did we catch?

Raising the threshold usually raises precision but lowers recall.

### Regression details

Fits a line or curve. Linear regression fits **y = w·x + b**, adjusting weight w and bias b with gradient descent until the average squared error is smallest.

### Why it matters

Most business ML is supervised: fraud detection, credit scoring, diagnosis, demand forecasting. **Main limit:** someone has to label the data, which can take thousands of human hours.

### Example

A bank trains a classifier on past transactions labeled "fraud" or "legit." A new card payment is scored in milliseconds and risky ones are blocked.

### Worked example: the confusion matrix

A spam filter checks 100 emails, of which 20 are really spam.

| | Predicted spam | Predicted not spam |
|---|---|---|
| **Actually spam (20)** | True positives (TP) = 15 | False negatives (FN) = 5 (missed spam) |
| **Actually not spam (80)** | False positives (FP) = 3 (good email blocked) | True negatives (TN) = 77 |

- **Accuracy** = (TP + TN) ÷ total = (15 + 77) ÷ 100 = **92%**
- **Precision** = TP ÷ (TP + FP) = 15 ÷ 18 = **83%**
- **Recall** = TP ÷ (TP + FN) = 15 ÷ 20 = **75%**
- **F1 score** = 2 × precision × recall ÷ (precision + recall) ≈ **0.79**. It balances the two in one number.

### Why accuracy alone can mislead

If only 1% of transactions are fraud, a model that always says "not fraud" is 99% accurate but catches nothing (recall = 0). For rare events, look at precision and recall.

Which error is worse depends on the job:
- Missing cancer (false negative) is worse than an extra check (false positive).
- A spam filter should avoid blocking real email (false positive).

### Common supervised algorithms in plain words

| Algorithm | How it works | Good for |
|-----------|--------------|----------|
| **Linear regression** | Fits a straight line through the data | Simple number predictions |
| **Logistic regression** | Squeezes a weighted sum into a probability between 0 and 1 | Yes/no decisions; easy to explain |
| **Decision tree** | A flowchart of yes/no questions ("income > $50K?") that ends in a prediction | Very easy to explain; can overfit |
| **Random forest** | Hundreds of trees trained on random samples of the data; they vote | Accurate and robust on tables of data |
| **Gradient boosting (XGBoost, LightGBM)** | Trees added one by one, each fixing the last one's mistakes | Often the best choice for tabular business data |
| **k-nearest neighbors (kNN)** | Looks at the k most similar past examples and copies their answer | Simple recommendations, small datasets |
| **Support vector machine (SVM)** | Draws the widest possible boundary between classes | Smaller datasets with clear separation |
| **Neural network** | Layers of weighted neurons (3.5) | Images, text, audio, huge datasets |

### Overfitting vs underfitting

| | Underfitting | Good fit | Overfitting |
|---|---|---|---|
| **What happens** | Model too simple; misses the pattern | Learns the real pattern | Model memorizes noise in the training data |
| **Training score** | Poor | Good | Excellent |
| **Test score** | Poor | Good | Poor |
| **Analogy** | Didn't study | Understood the topic | Memorized last year's answers |

This is the **bias-variance trade-off**: too simple = high bias (underfit); too sensitive to the training data = high variance (overfit).

### Ways to prevent overfitting

- More (and more varied) data
- Simpler models
- **Regularization** (penalizing very large weights)
- **Dropout** (randomly switching off neurons during training)
- **Early stopping** (stop when validation error starts rising)
- **k-fold cross-validation:** split the data into k parts, train on k−1 and test on the remaining one, rotate k times, and average the scores for a fairer estimate.

### Sources (from Research Notes)

- Google Machine Learning Crash Course
- Kirenz, Intro to classification (supervised learning basics)

---

## 3.3 Unsupervised Learning

### What it is

The model gets data with **no labels** and finds structure itself: groups, co-occurrences, or simpler ways to describe the data. IBM groups it into three main tasks: **clustering, association, and dimensionality reduction**.

### Why it matters

Most real-world data is unlabeled, and labeling is expensive. Unsupervised methods are used to explore data, segment customers, detect anomalies, and prepare data for other models.

### 1. Clustering

**What:** Grouping similar data points together.

**How (k-means):**
1. Choose k, the number of groups.
2. Place k center points (centroids) at random.
3. Assign every point to its nearest centroid.
4. Move each centroid to the average of its points.
5. Repeat steps 3–4 until the groups stop changing.

**Other methods:**
- **Hierarchical clustering:** builds a tree of nested groups.
- **DBSCAN:** finds dense regions and labels isolated points as noise, so it doesn't need k in advance.

**Example:** An online store clusters shoppers by spending and visit frequency into segments like "frequent small buyers" and "rare big spenders," then targets each with different offers.

### 2. Association

**What:** Finding rules like "customers who buy X also buy Y." Also called **market basket analysis**.

**How:** The **Apriori algorithm**, the most widely used method, first finds item sets that appear often, then builds rules from them.

Three measures judge a rule {A} → {B}:

| Metric | Definition |
|--------|------------|
| **Support** | How often A and B appear together across all baskets. |
| **Confidence** | Of baskets with A, the share that also have B. |
| **Lift** | Confidence divided by how common B is anyway. Lift > 1 means A really raises the chance of B; lift = 1 means no link. |

**Worked example:** If 75% of baskets with bread also contain butter, but butter is in 70% of all baskets anyway, lift is only about **1.07** — a weak link. A rule with lift 4 or 5 is worth acting on (shelf placement, bundles, "frequently bought together").

### 3. Dimensionality reduction

**What:** Shrinking many features into a few while keeping most of the information.

**How:**
- **PCA (principal component analysis)** finds the directions in which the data varies most and keeps only the top few.
- **t-SNE and UMAP** are non-linear methods mainly used to plot high-dimensional data in 2D.

**Why:** Fewer features means faster training, less noise, and data you can actually visualize.

**Example:** A survey with 50 questions can be reduced to 2–3 principal components (say "price sensitivity" and "brand loyalty") and plotted on a chart.

### Sources (from Research Notes)

- IBM, What is unsupervised learning?
- IBM, What is the Apriori algorithm?
- MathWorks, Introduction to Market Basket Analysis

---

## 3.4 Reinforcement Learning (RL)

### What it is

An **agent** learns by trial and error: it acts in an environment, gets a reward or penalty, and gradually learns a **policy** (a strategy) that earns the most reward over time. There are no labeled right answers, only feedback on how well things went.

### The RL loop

1. The agent observes the current state (e.g. the board position).
2. It picks an action using its policy.
3. The environment returns a reward and a new state.
4. The agent updates its policy to favor actions that led to higher total reward.
5. Repeat, often millions of times, usually in simulation.

### Key concepts

- **Exploration vs exploitation:** try new moves, or stick with what works.
- **Delayed reward:** a chess sacrifice only pays off many moves later.

### Algorithms

- Q-learning
- Deep Q-Networks (DQN)
- PPO

### Uses

- Games
- Robot movement
- Traffic-light timing
- Data-center cooling
- Aligning chatbots with **RLHF** (humans rank answers → a reward model learns their preferences → the language model is tuned to score well)

### Example: AlphaGo

DeepMind's AlphaGo beat world champion Lee Sedol 4–1 in Seoul in March 2016, using neural networks plus self-play. Its successor **AlphaGo Zero** learned purely by playing itself, with no human games at all.

### Watch out for: reward hacking

The agent finds a loophole. A boat-racing agent famously learned to spin in circles collecting bonus points instead of finishing the race.

### Sources (from Research Notes)

- Wikipedia, AlphaGo versus Lee Sedol
- Nature news: AlphaGo wraps up 4–1 victory
- Microsoft MSDN Magazine, Introduction to Reinforcement Learning
- BloomWiki, Reinforcement Learning (reward hacking)

---

## 3.5 Deep Learning and Neural Networks

### What it is

ML with artificial neural networks that have many layers ("deep" = many layers). Each layer learns a more abstract view: **edges → shapes → faces**. Unlike classical ML, you don't hand-pick the features.

### How a neural network works

1. **Neurons:** each one multiplies its inputs by weights, adds them up, and passes the result through an **activation function** (like ReLU).
2. **Layers:** an input layer, several hidden layers, and an output layer.
3. **Forward pass:** data flows through the network to produce a prediction.
4. **Backpropagation:** the error is sent backward through the network using calculus (the chain rule) to find how much each weight contributed.
5. **Gradient descent:** every weight is nudged slightly to reduce the error. Repeat over millions of examples.

### Main architectures

| Type | Best at | Example use |
|------|---------|-------------|
| **Feed-forward (MLP)** | Tabular data | Credit scoring |
| **CNN (convolutional)** | Images | Photo tagging, medical scans |
| **RNN / LSTM** | Sequences | Older speech and translation systems |
| **Transformer** | Language, and now images and audio | ChatGPT, Claude, Gemini |
| **GAN / diffusion** | Generating images | Midjourney, Stable Diffusion |

### Why it matters

Deep learning is behind almost every recent AI breakthrough: image recognition, speech assistants, translation and large language models. It needs lots of data and GPU computing power, which is why it took off only in the 2010s.

### Key milestones

- Backpropagation popularized by Rumelhart, Hinton and Williams (1986)
- **AlexNet** wins ImageNet (2012) with 15.3% top-5 error vs 26.2% for second place, trained on 1.2 million labeled photos with GPUs
- "Attention Is All You Need" introduces the Transformer (2017)
- Hinton and Hopfield win the Nobel Prize in Physics (2024)

### Example

AlexNet, trained on 1.2 million labeled ImageNet photos using GPUs, cut the error rate so sharply that computer vision switched to deep learning almost overnight.

### Training details to know

- **Activation functions** add non-linearity so networks can learn curves, not just straight lines.
  - **ReLU** outputs the input if positive, otherwise 0 (most common in hidden layers).
  - **Sigmoid** squeezes values to 0–1 (yes/no probability).
  - **Softmax** turns scores into probabilities that add up to 1 across many classes.
- **Learning rate:** how big each gradient-descent step is. Too big and training jumps around and never settles; too small and it takes forever.
- **Epoch:** one full pass through the training data.
- **Batch:** the small group of examples processed before each weight update.
- **Why GPUs:** training is mostly huge numbers of matrix multiplications that can run in parallel.
- **Transfer learning and fine-tuning:** start from a model already trained on a big general dataset, then train it a little more on your smaller, specific dataset. A hospital can fine-tune a general image model on a few thousand X-rays instead of millions.
- **Black box problem:** deep networks have millions or billions of weights, so it is hard to explain why they made a decision. **Explainable AI (XAI)** methods try to show which inputs mattered most.

### Sources (from Research Notes)

- Alom et al., The History Began from AlexNet (arXiv survey)
- Argonne ATPESC, Intro to Deep Learning slides (2026)
- Wikipedia, History of artificial neural networks
- Timeline of Deep Learning's Evolution

---

## 3.6 Predictive Analytics

### What it is

Using historical data, statistics and ML to estimate what will happen next: which customers will cancel, how much stock will sell, which transaction is fraud. It is the business application of the supervised learning from section 3.2.

### Where it sits among the four types of analytics

| Type | Question it answers | Example |
|------|---------------------|---------|
| **Descriptive** | What happened? | How many customers left last quarter |
| **Diagnostic** | Why did it happen? | Customers left after a price increase |
| **Predictive** | What is likely to happen? | Which customers will leave next month |
| **Prescriptive** | What should we do? | Offer those customers a discount |

### How it works

1. Define one precise question ("for each subscriber, what's the chance they don't renew in the next 30 days?").
2. Collect and clean historical data (sales, behavior, sensors).
3. Choose a model: classification for yes/no outcomes (churn, fraud), regression for amounts (sales, price), time-series models for forecasts over time.
4. Train and test on past data, measuring error.
5. Deploy, act on the predictions, and retrain as conditions change.

### Common techniques

- Logistic regression
- Decision trees
- Random forests
- Gradient-boosted trees (XGBoost, LightGBM)
- Time-series models like ARIMA
- Neural networks

### Why it matters

It turns data into decisions: fewer stockouts, earlier fraud alerts, and machines repaired before they break (predictive maintenance).

### The main weakness

"Garbage in, garbage out." Poor or biased data gives poor predictions, and models trained on the past can fail when the world changes suddenly.

### Example

A subscription company predicts each customer's churn risk every week and sends the highest-risk group a retention offer, instead of discounting everyone.

### Sources (from Research Notes)

- SAP, What is predictive analytics?
- Pecan AI, What Is Predictive Analytics?
- Kloepfel Consulting, Predictive Analytics lexicon

---

## 3.7 Computer Vision

### What it is

Teaching computers to understand images and video: what's in them, where things are, and what is happening. Almost all modern computer vision uses deep learning, especially CNNs and, more recently, vision transformers.

### Why it matters

Cameras are cheap and everywhere, so vision unlocks phone face unlock, medical scan reading, factory quality checks, self-checkout and self-driving cars.

### Main tasks

| Task | Question | Output |
|------|----------|--------|
| **Image recognition (classification)** | What is in this picture? | One label, e.g. "dog" |
| **Object detection** | What objects are here, and where? | A box + label for each object |
| **Segmentation** | Which exact pixels belong to each object? | A pixel-level outline |
| **Video analysis** | What is happening over time? | Tracks, actions, events |

### Image recognition

**How:** A CNN scans the image with small filters that detect edges, then textures, then parts, then whole objects, and outputs a probability for each class. Models are trained on huge labeled datasets like ImageNet (1.2 million photos, 1,000 classes).

**Example:** Google Photos letting you search your gallery for "beach" or "cat"; doctors' tools flagging possible tumors in X-rays.

### Object detection

**How:** The model must do two jobs at once: **localize** (draw a box) and **classify** (name it). Older two-stage detectors (R-CNN family) first proposed regions and then classified each one. **YOLO** ("You Only Look Once," 2015) splits the image into a grid and predicts all boxes and labels in one pass, fast enough for live video.

**Example:** A photo of three dogs gets one label ("dog") from a classifier, but three separate labeled boxes from a detector. Self-driving cars detect pedestrians, cars and signs many times per second.

### Video analysis

**How:** Run detection on each frame, then link the same object across frames (tracking, often with a **Kalman filter** that predicts where it will move next). On top of tracks, models can recognize actions (running, falling) or count events.

**Example:** Sports analytics tracking every player's position; traffic cameras counting cars; stores spotting empty shelves.

### Limits

Models can fail on lighting, angles or groups of people underrepresented in training data, and face recognition raises serious privacy and surveillance concerns.

### Sources (from Research Notes)

- Fritz AI glossary, Object Detection
- Augmented Startups, Beginner's Guide to Object Detection
- NIH/PMC, Object detection framework using YOLOv8 for road video
- NIH/PMC, Object detectors for visual object tracking

---

## 3.8 Robotics and Autonomous Systems

### What it is

Robotics puts AI into a physical body that senses, decides and acts in the real world. An **autonomous system** does this without a human controlling each step, such as a self-driving car, warehouse robot or delivery drone. It combines everything above: computer vision to see, prediction to anticipate, and RL or deep learning to decide.

### The robot stack

| Stage | What happens |
|-------|--------------|
| **1. Perceive** | Cameras, lidar, radar and touch sensors, interpreted with computer vision. |
| **2. Localize & map** | Work out where it is (often **SLAM**, simultaneous localization and mapping). |
| **3. Plan** | Choose a path or sequence of moves (motion planning). |
| **4. Control** | Turn the plan into motor commands (robot control). |
| **5. Learn** | Improve from data and experience (robot learning). |

### Robot control

**What:** The low-level loop that makes motors do what the plan says, hundreds of times per second.

**How:** A feedback controller compares where the robot is with where it should be and corrects the error. The classic **PID controller** reacts to the current error (P), the error built up over time (I), and how fast the error is changing (D, "if I'm about to overshoot, slow down"). Optimal controllers such as **LQR** and **MPC** plan the best commands under physical limits.

**Example:** A drone keeping steady in wind; a robot arm stopping exactly on a weld point.

### Motion planning

**What:** Finding a collision-free path from start to goal that the robot's body can actually follow.

**How:**
- **A\*** searches a grid map for the shortest route, using a distance estimate to the goal to search efficiently.
- **RRT / RRT\*** (rapidly-exploring random trees) grow a tree of random sample points through space, which works well for robot arms with many joints.
- Newer methods use neural networks to guide where to sample.

**Example:** A warehouse robot routing around shelves and other robots; a self-driving car planning a lane change.

### Robot learning

**What:** Robots acquiring skills from data instead of hand-coded rules.

**How:**
- **Imitation learning:** learn by copying human demonstrations, e.g. a person guides the arm or teleoperates it (**behavior cloning**).
- **Reinforcement learning:** practice by trial and error, usually in a physics simulator first, then transfer to the real robot (**sim-to-real**).
- **Foundation models for robots:** large vision-language-action models trained on many robots' data so one model can follow instructions like "put the apple in the bowl."

**Example:** Robots learning to grasp unfamiliar objects or fold laundry after watching demonstrations.

### Swarm robotics

**What:** Many simple robots cooperating through local rules, with no central leader, inspired by ants, bees and bird flocks. If a few robots fail, the group still works.

**How:** Each robot only senses and talks to its neighbors. Simple shared rules (stay close, avoid collisions, follow a signal gradient) produce complex group behavior. This is called **emergent behavior**.

**Example:** Harvard's **Kilobots** (2014): 1,024 coin-sized robots costing about $20 each. Given a target shape and four "seed" robots as a reference point, they used three behaviors (edge-following, gradient counting and neighbor-based localization) to arrange themselves into a star or a wrench in about 12 hours, with no human help. Future uses include search-and-rescue, crop monitoring and drone light shows.

### Why it matters

- The IFR's World Robotics 2026 report counts a record **5 million industrial robots** working in factories in 2025, with installations up 11% to over 600,000. China installed 354,000 of them (59% of the world total).
- **Waymo** was giving about **500,000 paid driverless rides per week** by March 2026, targeting 1 million by the end of 2026.

### Challenges across robotics

Safety around people, unpredictable real-world conditions, cost, and who is responsible when an autonomous system makes a mistake.

### Sources (from Research Notes)

- Australian Manufacturing, IFR World Robotics 2026 report summary
- Bloomberg, Waymo co-CEO on 1 million weekly trips
- ai2.work, Waymo hits 500,000 weekly rides
- Univ. of Washington CSE 571, Motion planning to PID and LQR
- Diehl et al., Imitation Learning for Robot Motion Planning and Control (arXiv)
- National Geographic, A Swarm of a Thousand Self-Organising Robots

---

## Try it yourself

### Activity 3.1 · Supervised, unsupervised or reinforcement? (card sort)

Sort these:

(a) Spam filter trained on labeled emails
(b) Grouping shoppers into segments
(c) A robot learning to walk by trial and error
(d) Predicting house prices
(e) "Customers who bought X also bought Y"
(f) A game AI that improves by playing itself

**Answers:**
- (a) supervised
- (b) unsupervised
- (c) reinforcement
- (d) supervised (regression)
- (e) unsupervised (association)
- (f) reinforcement

---

### Activity 3.2 · Be the evaluator (pen and paper)

A spam filter checks 50 emails; 10 are spam. It flags 8 emails, and 6 of those are really spam. Fill in the confusion matrix and calculate precision and recall.

**Answers:**
- TP = 6
- FP = 2
- FN = 4
- TN = 38
- Precision = 6 ÷ 8 = **75%**
- Recall = 6 ÷ 10 = **60%**

---

## KEY TAKEAWAYS

- ML finds rules from data; the training loop is collect → model → train → test → deploy.
- Supervised = labels; unsupervised = no labels (clustering, association, PCA); RL = rewards.
- Deep learning stacks layers and learns with backpropagation + gradient descent.
- Applications: predictive analytics, computer vision, robotics.

---

## Key terms

| Term | Definition |
|------|------------|
| **Feature / label** | An input variable / the correct answer in training data. |
| **Overfitting** | Memorizing training data instead of learning the general pattern. |
| **Loss function** | A score of how wrong the predictions are. |
| **Gradient descent** | Adjusting parameters step by step to reduce loss. |
| **Backpropagation** | Sending the error backward through a network to update weights. |
| **Policy** | An RL agent's strategy for choosing actions. |
| **Bounding box** | Rectangle marking an object's location in an image. |
| **SLAM** | A robot building a map while tracking its own position. |
| **Hyperparameter** | A setting chosen before training, like the learning rate. |
| **Confusion matrix** | Table of true/false positives and negatives. |
| **F1 score** | One number balancing precision and recall. |
| **Underfitting** | A model too simple to learn the pattern. |
| **Cross-validation** | Rotating which part of the data is used for testing, then averaging. |
| **Regularization** | Penalizing complexity to reduce overfitting. |
| **Activation function** | Non-linear step in a neuron (ReLU, sigmoid, softmax). |
| **Epoch** | One full pass through the training data. |
| **Transfer learning** | Reusing a pretrained model for a new task. |
| **Emergent behavior** | Group behavior arising from simple individual rules. |

---

## Complete Sources List (from Research Notes)

1. Forbes via AITopics: Samuel and the origin of "machine learning"
2. Stanford HAI, 2026 AI Index Report
3. Google Machine Learning Crash Course
4. IBM, What is unsupervised learning?
5. IBM, What is the Apriori algorithm?
6. Wikipedia, AlphaGo versus Lee Sedol
7. Microsoft MSDN Magazine, Introduction to Reinforcement Learning
8. Alom et al., The History Began from AlexNet (arXiv)
9. Argonne ATPESC, Intro to Deep Learning (2026)
10. SAP, What is predictive analytics?
11. Fritz AI glossary, Object Detection
12. NIH/PMC, YOLOv8 road video detection framework
13. Australian Manufacturing, IFR World Robotics 2026
14. Bloomberg, Waymo path to 1 million weekly trips
15. Univ. of Washington CSE 571, Motion planning and control
16. National Geographic, Kilobot swarm
17. IBM, Natural language processing
18. Wikipedia, History of natural language processing
19. NLPplanet, 33 important NLP tasks explained
20. TechCrunch, Google brings in BERT to improve its search results
21. MobileSyrup, Google Search and conversational queries (BERT)
22. Wikipedia, Word2vec
