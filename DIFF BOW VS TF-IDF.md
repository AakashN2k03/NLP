# Bag of Words vs TF-IDF

| Feature | **BoW (Bag of Words)** | **TF-IDF** |
|---------|------------------------|------------|
| What it does | Counts how many times each word appears in a document | Weighs words by how **important** they are in the document |
| Type | Frequency-based model | Weighted frequency model |

## 📊  Example

### 📄 Documents
```
Doc 1: "I love NLP" 
Doc 2: "I love machine learning and NLP"
```

### ✅ Vocabulary
```
[i, love, nlp, machine, learning, and]
```

### 🧮 BoW Representation

| Word | Doc 1 | Doc 2 |
|------|-------|-------|
| i | 1 | 1 |
| love | 1 | 1 |
| nlp | 1 | 1 |
| machine | 0 | 1 |
| learning | 0 | 1 |
| and | 0 | 1 |

Just raw **counts**. Every word is treated equally.

### 🧮 TF-IDF Representation (Simplified)

TF-IDF = **TF × IDF**, where:
* **TF (Term Frequency)** = How often a word appears in a document
* **IDF (Inverse Document Frequency)** = Penalizes words that appear in **many documents**

In our case:
* Common words like **"I", "love", "NLP"** appear in both → **lower weight**
* Rare words like **"machine", "learning", "and"** appear only in Doc 2 → **higher weight**

So:

| Word | Doc 1 (TF-IDF) | Doc 2 (TF-IDF) |
|------|----------------|----------------|
| i | low | low |
| love | low | low |
| nlp | low | low |
| machine | 0 | high |
| learning | 0 | high |
| and | 0 | high |

## 🔍 3. Key Differences

| Aspect | **Bag of Words (BoW)** | **TF-IDF** |
|--------|------------------------|------------|
| Counts | Raw word counts | Weighted by rarity (IDF) |
| Common Words | Given equal importance | Penalized (low score) |
| Rare Words | Same as others | Boosted (high score) |
| Result | Sparse matrix with raw frequencies | Sparse matrix with weighted scores |
| Use Cases | Simple models like Naive Bayes | Better for SVM, Logistic Regression |
| Context awareness | ❌ No context | ❌ Still no context, but better word weighting |
| Computation time | 🟢 Fast | 🟡 Slightly slower (due to IDF computation) |

## ✅ When to Use What?

| Situation | Go For |
|-----------|--------|
| Simple model or small data | BoW |
| Better accuracy & filtering common words | TF-IDF |
| Need contextual understanding | ❌ Neither (Use Word2Vec, BERT, etc.) |

## Why Is **TF-IDF** Better Than BoW?

### ✅ 1. **Reduces Impact of Common Words**

**BoW:**
* Treats all words equally.
* Words like "is", "the", "and" are high in frequency, but not meaningful.
* These dominate the feature space.

**TF-IDF:**
* Downweights such common words using **IDF**.
* Helps highlight **important**, **topic-specific** words.
