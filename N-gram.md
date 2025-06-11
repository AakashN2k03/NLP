## 1. What is an N-gram?

An **n-gram** is a **sequence of 'n' consecutive items** from a given text. These items are typically **words** or **characters**.

* **Unigram (n=1)** → Single words
* **Bigram (n=2)** → Pairs of words  
* **Trigram (n=3)** → Triplets of words
* **4-gram (n=4)** → Four-word sequences, and so on

### Example

Given the sentence: `"I love machine learning"`

| Type | n-grams |
|------|---------|
| **Unigram** | `["I", "love", "machine", "learning"]` |
| **Bigram** | `["I love", "love machine", "machine learning"]` |
| **Trigram** | `["I love machine", "love machine learning"]` |

## 2. Why are N-grams Useful?

N-grams help **capture the context** and **structure of language**, especially for tasks where **word order matters**. They provide a way to model the probability of word sequences and understand linguistic patterns.

## 3. Where Does It Come in NLP?

📌 N-grams are studied under **Natural Language Processing (NLP)**

**Subtopics include:**
* Text preprocessing
* Language modeling
* Text classification
* Text generation
* Vectorization (feature extraction)

## 4. Applications of N-grams

| Application | Use of N-grams |
|-------------|----------------|
| 🔡 **Autocomplete** | Predict the next word based on previous words |
| 📬 **Spam Detection** | Analyze patterns in email text using n-gram frequency |
| 📘 **Language Modeling** | Probability models of word sequences |
| 🤖 **Chatbots** | Improve understanding of user input context |
| 📈 **Sentiment Analysis** | Capture phrases like "not good", "very happy", etc. |
| 🔁 **Machine Translation** | Learn word group structures and grammar |

## 5. Code Example in Python (Using NLTK)

```python
import nltk
from nltk.util import ngrams
from nltk.tokenize import word_tokenize

sentence = "I love machine learning"
tokens = word_tokenize(sentence)

# Unigrams
unigrams = list(ngrams(tokens, 1))
print("Unigrams:", unigrams)

# Bigrams
bigrams = list(ngrams(tokens, 2))
print("Bigrams:", bigrams)

# Trigrams
trigrams = list(ngrams(tokens, 3))
print("Trigrams:", trigrams)
```

**Output:**
```bash
Unigrams: [('I',), ('love',), ('machine',), ('learning',)]
Bigrams: [('I', 'love'), ('love', 'machine'), ('machine', 'learning')]
Trigrams: [('I', 'love', 'machine'), ('love', 'machine', 'learning')]
```

## 6. Limitations of N-grams

| Limitation | Explanation |
|------------|-------------|
| ❌ **Data sparsity** | As n increases, rare combinations become frequent |
| ❌ **Fixed window size** | N-grams can't model long-term dependencies |
| ❌ **Memory and computation cost** | Higher n = more memory needed for storing sequences |
| ❌ **Context loss** | Limited to fixed-size windows, missing broader context |
| ❌ **Out-of-vocabulary words** | Struggles with unseen word combinations |
