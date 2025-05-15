# 📘 Word Embedding in NLP

## 🧠 Overview

**Word embedding** is a technique used in **Natural Language Processing (NLP)** to represent words as **dense, numerical vectors** that capture their **meanings** and **relationships** with other words.

---

## 🔑 Key Points

- Each word is mapped to a **vector of real numbers** (typically 100 or 300 dimensions).
- **Similar words** have **similar vectors** (e.g., `"king"` and `"queen"`).
- It helps machines understand the **meaning** and **context** of words.
- These vectors are **learned from large text data** using models like:
  - **Word2Vec**
  - **GloVe**
  - **FastText**

---

## 🧮 Example

The classic example that shows how word embeddings capture **semantic relationships**:

- vec("king") - vec("man") + vec("woman") ≈ vec("queen")


This works because the embedding captures gender and role-related meaning.

---

## 🔍 Word Embedding vs. Vectorization

| Feature               | Vectorization                                   | Word Embedding                                               |
|-----------------------|--------------------------------------------------|---------------------------------------------------------------|
| **Definition**        | Converting words or documents into numerical vectors | Special type of vectorization that creates dense, meaningful vectors |
| **Goal**              | Make text machine-readable                       | Capture semantic meaning and relationships between words     |
| **Examples**          | One-Hot, BoW, TF-IDF                             | Word2Vec, GloVe, FastText, BERT                              |
| **Dense or Sparse?**  | Usually sparse (mostly 0s)                       | Always dense (compact, low-dimensional)                      |
| **Learns from data?** | ❌ No – just counts or positions                 | ✅ Yes – trained from context or co-occurrence               |
| **Captures meaning?** | ❌ No                                            | ✅ Yes                                                       |
| **Context-aware?**    | ❌ No                                            | ✅ Yes (in models like BERT, GPT)                            |
| **Used in NLP today?**| Rarely (used in simple models)                  | ✅ Widely used in modern NLP models                          |

---

## 🤓 Simplified Understanding

- **Vectorization** = Any method to convert text into numbers (**broad umbrella**).
- **Word Embedding** = Smart, dense, and learned representation (**subset of vectorization**).

---

## 🧰 Common Techniques

### 📦 Vectorization Techniques:
- One-Hot Encoding
- Bag of Words (BoW)
- TF-IDF

### 💡 Word Embedding Techniques (subset of vectorization):
- Word2Vec
- GloVe
- FastText
- BERT / GPT Embeddings

---

> 📝 Word embeddings are fundamental to modern NLP applications including chatbots, sentiment analysis, machine translation, and more.

