# 05 Natural Language Processing

How AI reads, understands and produces human language, in text or speech.

---

## What NLP is

NLP is the branch of AI that lets computers read, understand and produce human language. IBM describes it as combining **computational linguistics** (the rules of language) with **statistical machine learning and deep learning**.

Chatbots, translation apps, voice assistants and search engines all run on it.

### Expanded context from Research Notes

NLP is the branch of AI that lets computers read, understand and produce human language, in text or speech. IBM describes it as combining computational linguistics (the rules of language) with statistical machine learning and deep learning. Chatbots, translation apps, voice assistants and search engines all run on it.

Large language models like ChatGPT are the newest, biggest form of NLP.

---

## How it works: five steps

1. **Clean and tokenize:** split text into tokens (words or word pieces). "I loved it!" → I / loved / it / !
2. **Normalize:** reduce words to a base form (**lemmatization:** "loved" → "love") and label grammar (**part-of-speech tagging:** noun, verb, adjective).
3. **Turn words into numbers:** each token becomes a vector called an **embedding**. Words used in similar ways get similar vectors, so "good" is closer to "great" than to "table."
4. **Model the meaning:** today usually a Transformer reads the whole sentence and works out how the words relate.
5. **Produce an output:** a label (positive review), extracted facts (names, dates), or new text (translation, summary, chatbot reply).

### Preprocessing details

- **Stop words:** very common words ("the," "is," "and") that older systems often removed to save space. Modern models keep them, because small words carry meaning ("to" in the BERT visa example).
- **Stemming vs lemmatization:** stemming chops word endings with simple rules ("studies" → "studi"); lemmatization uses a dictionary to find the real base word ("studies" → "study," "better" → "good"). Lemmatization is slower but more accurate.
- **n-grams:** groups of n words in a row ("New York" is a 2-gram). They let older models capture short phrases.
- **Subword tokenization:** modern LLMs split rare words into common pieces, e.g. "unbelievably" → un / believe / ably (methods like byte-pair encoding). The model can then handle new words, typos and names without needing every word in its vocabulary.

### Expanded context from Research Notes

1. **Clean and tokenize:** split text into tokens (words or word pieces), e.g. "I loved it!" becomes I / loved / it / !
2. **Normalize:** reduce words to a base form (lemmatization: "loved" becomes "love") and label each word's grammar (part-of-speech tagging: noun, verb, adjective).
3. **Turn words into numbers:** each token becomes a vector called an embedding. Words used in similar ways get similar vectors, so the model can tell "good" is closer to "great" than to "table".
4. **Model the meaning:** a model (today usually a Transformer, see the LLM section) reads the whole sentence and works out how the words relate.
5. **Produce an output:** a label (positive review), extracted facts (names, dates), or new text (a translation, a summary, a chatbot reply).

---

## Main NLP tasks

| Task | What it does | Everyday example |
|------|--------------|------------------|
| **Text classification** | Puts a document into a category | Spam filter |
| **Sentiment analysis** | Decides if text is positive or negative | Rating product reviews |
| **Named entity recognition (NER)** | Finds names of people, places, companies, dates | Pulling flight details from an email |
| **Part-of-speech tagging** | Labels each word's grammatical role | Grammar checkers |
| **Machine translation** | Converts one language into another | Google Translate |
| **Question answering** | Answers a question in natural language | Search engines, AI Overviews |
| **Summarization** | Shortens text but keeps the meaning | Meeting-note summaries |
| **Speech → text** | Converts between voice and text | Siri, Alexa, auto captions |

### Expanded context from Research Notes

| Task | What it does | Everyday example |
|------|--------------|------------------|
| **Text classification** | Puts a document into a category | Spam filter |
| **Sentiment analysis** | Decides if text is positive or negative | Rating product reviews |
| **Named entity recognition (NER)** | Finds names of people, places, companies, dates | Pulling flight details from an email |
| **Part-of-speech tagging** | Labels each word's grammatical role | Grammar checkers |
| **Machine translation** | Converts one language into another | Google Translate |
| **Question answering** | Answers a question in natural language | Search engines, AI Overviews |
| **Summarization** | Shortens text but keeps the meaning | Meeting-note summaries |
| **Speech-to-text / text-to-speech** | Converts between voice and text | Siri, Alexa, auto captions |

---

## How NLP evolved: three eras

| Era | Key events |
|-----|------------|
| **Rules (1950s–1980s)** | Experts hand-wrote grammar rules. The 1954 Georgetown-IBM experiment translated 60+ Russian sentences into English. ELIZA (Joseph Weizenbaum, MIT, 1964–66) imitated a therapist with a few pattern rules. In 1966 the ALPAC report judged machine translation disappointing and funding was cut. |
| **Statistics (late 1980s–2000s)** | Models learned word patterns from large amounts of text instead of rules, e.g. IBM's statistical translation models (1993). |
| **Deep learning (2013–now)** | word2vec (Google, 2013) learned word embeddings; Transformers (2017), BERT and GPT made understanding far more accurate. In October 2019 Google added BERT to Search (~1 in 10 US English searches). |

### Expanded context from Research Notes

- **Rules (1950s–1980s):** experts hand-wrote grammar rules. The 1954 Georgetown-IBM experiment automatically translated more than 60 Russian sentences into English. ELIZA (Joseph Weizenbaum, MIT, 1964–66) imitated a therapist using a few pattern rules. In 1966 the ALPAC report judged machine translation disappointing and funding was sharply cut.
- **Statistics (late 1980s–2000s):** instead of rules, models learned word patterns from large amounts of text, e.g. IBM's statistical translation models (1993).
- **Deep learning (2013–now):** word2vec (Google, 2013) learned word embeddings from text; Transformers (2017) and models like BERT and GPT made language understanding far more accurate. In October 2019 Google added BERT to Search, affecting about 1 in 10 English searches in the US.

---

## The BERT example

You type "2019 brazil traveler to usa need a visa." Older keyword matching ignored the small word "to" and showed results about US citizens going to Brazil. BERT reads the whole sentence in context, understands the traveler is going to the USA, and returns the right visa page. This was Google's own launch example.

### Expanded context from Research Notes

You type "2019 brazil traveler to usa need a visa" into Google. Older keyword matching ignored the small word "to" and showed results about US citizens going to Brazil. BERT reads the whole sentence in context, understands the traveler is going to the USA, and returns the right visa page. This was Google's own launch example for BERT.

---

## From counting words to understanding meaning

| Representation | How it works | Weakness |
|----------------|--------------|----------|
| **One-hot** | Each word is a long list of zeros with a single 1 in its own position | No idea that "good" and "great" are related |
| **Bag of words** | A document becomes counts of each word, ignoring order | "Dog bites man" = "man bites dog" |
| **TF-IDF** | Weights words that are frequent in this document but rare overall, so "the" scores low and "photosynthesis" scores high | Still no meaning or order; long used in classic search ranking |
| **Word embeddings (word2vec, 2013)** | Each word gets a dense vector learned from the words around it. Directions capture meaning: king − man + woman ≈ queen | One vector per word: "bank" (river) and "bank" (money) look the same |
| **Contextual embeddings (BERT, GPT)** | The vector for a word changes with the sentence, so the two "banks" get different vectors | Needs large Transformer models and lots of computing |

### Expanded context from Research Notes

The Research Notes describe how text representation evolved:

- **One-hot and bag of words** count words with no meaning or order.
- **TF-IDF** weights words that are frequent in this document but rare overall.
- **word2vec (2013)** learned dense meaning vectors (king − man + woman ≈ queen) but one vector per word.
- **Contextual embeddings** from BERT/GPT change with the sentence, so ambiguous words like "bank" get the right meaning.

---

## Sequence models: from RNNs to attention

### RNNs (recurrent neural networks)

Read text one word at a time, carrying a "memory" forward. **Problem:** by the end of a long sentence they forget the start.

### LSTM (long short-term memory)

Added gates that decide what to keep or forget, and powered translation and speech systems in the mid-2010s (e.g. Google Translate's 2016 neural system).

### Sequence-to-sequence (seq2seq)

An **encoder** reads the input sentence and a **decoder** writes the output, used for translation. Squeezing a whole sentence into one memory was a bottleneck.

### Attention (2014)

Let the decoder look back at every input word when writing each output word.

### The Transformer (2017)

Kept only attention, dropped the slow word-by-word reading, and became the basis of modern NLP (Topic 4).

### Expanded context from Research Notes (LLM section)

The Transformer architecture ("Attention Is All You Need," Google, 2017) uses **self-attention**: for each token, the model scores how relevant every other token is and blends in their information. In "The animal didn't cross the street because it was too tired," attention helps link "it" to "animal." Unlike older RNNs, which read one word at a time, Transformers process all tokens at once. That made training on huge datasets with GPUs practical.

---

## BERT vs GPT

| | BERT (Google, 2018) | GPT (OpenAI, 2018 onwards) |
|---|---|---|
| **Part of the Transformer** | Encoder | Decoder |
| **Training task** | Fill in blanked-out words ("masked language modeling"), reading both left and right context | Predict the next word, reading left to right |
| **Best at** | Understanding: search ranking, classification, entity recognition | Generating: writing, chat, summaries, code |
| **Example use** | Google Search query understanding (2019) | ChatGPT |

### Expanded context from Research Notes

BERT (Google, 2018) is a Transformer encoder trained to fill in masked words using both left and right context; best at understanding (search ranking, classification, NER), e.g. Google Search 2019.

GPT is a decoder trained to predict the next word left to right; best at generating text, e.g. ChatGPT.

---

## Speech: how a voice assistant works

1. **Wake word detection** ("Hey Siri") runs on the device.
2. **Automatic speech recognition (ASR)** turns audio into text.
3. **Natural language understanding (NLU)** finds the intent ("set an alarm") and slots or details ("7 a.m. tomorrow").
4. The system acts or looks up an answer.
5. **Text-to-speech (TTS)** speaks the reply.

### Newer developments

Newer voice modes in assistants like ChatGPT and Gemini increasingly handle audio directly with one multimodal model, which sounds more natural but makes sources harder to show (Topic 10).

### Expanded context from Research Notes

This five-step process is the same pipeline described in the Study Guide. The Research Notes add that newer voice modes use one multimodal model, which sounds more natural but makes sources harder to show.

---

## How chatbots evolved

| Generation | How it works | Example |
|------------|--------------|---------|
| **Rule-based** | Pattern matching and scripted replies | ELIZA (1960s) |
| **Intent-based** | Classify the intent, fill slots, give a pre-written answer or action | Early Siri/Alexa, bank help bots |
| **Generative (LLM)** | Writes a new reply word by word, can use search and tools | ChatGPT, Claude, Gemini, Klarna's assistant |

### Expanded context from Research Notes

- **Rule-based:** pattern matching and scripted replies (ELIZA, 1960s).
- **Intent-based:** classify the intent, fill slots, give a pre-written answer or action (early Siri/Alexa, bank help bots).
- **Generative (LLM):** writes a new reply word by word, can use search and tools (ChatGPT, Claude, Gemini, Klarna's assistant).

---

## How NLP systems are measured

| Task | Common metric | What it checks |
|------|---------------|----------------|
| Classification, sentiment, NER | Accuracy, precision, recall, F1 | Correct labels (as in Topic 3) |
| Machine translation | BLEU | Overlap of words and phrases with human translations |
| Summarization | ROUGE | How much of a reference summary's wording is covered |
| Speech recognition | Word error rate (WER) | Share of words wrong, missing or added |
| Chat and open answers | Human ratings, LLM-as-a-judge, faithfulness | Helpfulness and accuracy (Topic 8) |

### The problem with word-overlap metrics

Word-overlap scores like BLEU and ROUGE are quick but miss meaning: a correct answer worded differently scores low, which is why human and model-based judging is used for LLMs.

### Expanded context from Research Notes

The Research Notes mention that BLEU is for translation, ROUGE is for summarization, and WER is for speech recognition. Human and LLM-based judging are used for open-ended chat answers because word-overlap metrics miss meaning.

---

## Why it matters

Most of the world's information is **unstructured text** (emails, documents, web pages, posts). NLP lets machines search, sort and summarize it at scale, and lets people use computers by typing or speaking.

### Real-world impact

IBM reports one insurer cut text-analysis work by **90%** with language models.

### Expanded context from Research Notes

Most of the world's information is unstructured text: emails, documents, web pages, social posts. NLP lets machines search, sort and summarize it at scale, and lets people use computers by simply typing or speaking. IBM reports one insurer cut text-analysis work by 90% with language models.

---

## Hard cases (watch out for)

- **Ambiguity:** "I saw her duck." (Duck could be a bird or an action.)
- **Sarcasm:** "Great, another Monday."
- **Slang and emojis.**
- **Low-resource languages** with less training data get weaker results.
- **Bias** copied from the text a model learned from.

### Expanded context from Research Notes

- **Ambiguity:** "I saw her duck" (duck could be a bird or an action).
- **Sarcasm:** "Great, another Monday" (literal words are positive; meaning is negative).
- **Slang and emojis.**
- **Low-resource languages** with less training data get weaker results.
- **Bias** copied from the text a model learned from.

---

## Try it yourself

### Activity 5.1 · Tokenize and tag (paper)

Take "I didn't love the ending, but the acting was great!" Split it into tokens, circle the words that carry sentiment, and decide the overall sentiment.

**What to notice / answers:** "didn't" flips "love," and "but" shifts the focus. Simple word counting would get this wrong; context matters.

---

### Activity 5.2 · Ambiguity test (try with a chatbot)

Ask a chatbot what "I saw her duck" means. Then ask it to translate "I went to the bank" into another language you know.

**What to notice / answers:** Does it notice there are two meanings, or pick one silently? Good systems ask or explain.

---

## KEY TAKEAWAYS

- Pipeline: tokenize → normalize → embed → model meaning → output.
- Eras: rules (ELIZA) → statistics → deep learning (word2vec, Transformers, BERT, GPT).
- LLMs are the newest form of NLP, which is why AI Overviews can answer in plain language.

---

## Key terms

| Term | Definition |
|------|------------|
| **Token / tokenization** | A word or word piece / splitting text into them. |
| **Lemmatization** | Reducing a word to its base form ("loved" → "love"). |
| **Embedding** | A number vector capturing a word's meaning. |
| **Named entity** | A name of a person, place, company or date. |
| **Sentiment** | Whether text is positive or negative. |
| **Stop words** | Very common words like "the" and "is." |
| **Stemming** | Chopping word endings by rule ("studies" → "studi"). |
| **n-gram** | A sequence of n words in a row. |
| **TF-IDF** | Word weight: frequent in this document, rare elsewhere. |
| **Contextual embedding** | A word vector that changes with the sentence. |
| **RNN / LSTM** | Networks that read text one word at a time with memory. |
| **Encoder / decoder** | The parts that read input / write output. |
| **Intent and slots** | What a user wants, and the details needed to do it. |
| **BLEU / ROUGE / WER** | Metrics for translation, summarization and speech. |
| **Corpus** | A large collection of text. |

---

## Sources (from Research Notes)

- IBM, Natural language processing
- Wikipedia, History of natural language processing
- NLPplanet, 33 important NLP tasks explained
- TechCrunch, Google brings in BERT to improve its search results (2019)
- MobileSyrup, Google Search now better understands conversational queries (2019)
- Wikipedia, Word2vec
