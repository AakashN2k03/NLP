# Bag of Words (BoW)

Bag of Words (BoW) is one of the simplest and most widely used techniques for text representation in Natural Language Processing (NLP). It converts a text document into a numerical vector, which can be used by machine learning algorithms.

Think of BoW as a way to count how often each word appears in a document, ignoring grammar and word order.

## 🧠 Key Concepts

1. **Vocabulary**: The set of all unique words in your dataset.
2. **Frequency**: The number of times each word appears in a document.
3. **Vector Representation**: Each document becomes a vector where each dimension corresponds to a word in the vocabulary.

## 📄 Example: Step-by-Step

Suppose we have 2 simple sentences:

```
Doc 1: "I love machine learning"
Doc 2: "Machine learning is fun"
```

### 🔹 Step 1: Preprocessing
Convert to lowercase, remove punctuation, stopwords (optional), etc.

```
Doc 1: [i, love, machine, learning]
Doc 2: [machine, learning, is, fun]
```

### 🔹 Step 2: Create Vocabulary

```
Vocabulary = [i, love, machine, learning, is, fun]
Indices =    [0, 1,    2,        3,     4,  5]
```

### 🔹 Step 3: Create Vector for Each Document

| Word     | Doc 1 | Doc 2 |
|----------|-------|-------|
| i        | 1     | 0     |
| love     | 1     | 0     |
| machine  | 1     | 1     |
| learning | 1     | 1     |
| is       | 0     | 1     |
| fun      | 0     | 1     |

So,

```
Doc 1 → [1, 1, 1, 1, 0, 0]
Doc 2 → [0, 0, 1, 1, 1, 1]
```

## ✅ Advantages

- Simple and easy to implement
- Works well for small datasets
- Good baseline for NLP tasks

## ❌ Limitations

| Limitation | Explanation |
|------------|-------------|
| No context | Word order is ignored (e.g., "dog bites man" vs "man bites dog") |
| Sparse vectors | Long vectors with mostly zeros if vocab is large |
| Vocabulary growth | Gets very large with big corpora |
| Same weights for common vs rare words | Doesn't consider importance (TF-IDF solves this) |

## 🤖 Real-World Use Cases

- **Text Classification**: Spam vs Ham
- **Sentiment Analysis**: Positive vs Negative review
- **Information Retrieval**: Search engines

## 💻 Basic Implementation (Python)

```python
from sklearn.feature_extraction.text import CountVectorizer

# Example documents
documents = [
    "I love machine learning",
    "Machine learning is fun"
]

# Create a Bag of Words representation
vectorizer = CountVectorizer()
X = vectorizer.fit_transform(documents)
