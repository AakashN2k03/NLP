# 🧠 CBOW Word2Vec Model

This repository implements the **Continuous Bag of Words (CBOW)** model, a variant of Word2Vec that learns word embeddings by predicting a target word from its surrounding context words.

## 📋 Table of Contents
- [Overview](#overview)
- [What is CBOW?](#what-is-cbow)
- [Architecture](#architecture)
- [Implementation Process](#implementation-process)
- [Example Walkthrough](#example-walkthrough)
- [Applications](#applications)
- [Advantages and Limitations](#advantages-and-limitations)

## Overview

CBOW (Continuous Bag of Words) is a powerful natural language processing technique that creates dense vector representations of words (word embeddings) by learning to predict a target word from its surrounding context words. These word embeddings capture semantic relationships between words, allowing similar words to have similar vector representations.

## What is CBOW?

CBOW is a shallow neural network used in Natural Language Processing (NLP) that aims to predict a **target word** given a set of **context words**.

> 🧾 Example:  
> Sentence: "I love coding everyday"  
> Target word: `"coding"`  
> Context words (window=1): `"love"`, `"everyday"`  
> CBOW tries to predict `"coding"` from `"love"` and `"everyday"`

## Architecture

The CBOW model follows this architecture:

Input (context) → Embedding Layer (W) → Averaging → Output Layer (W') → Softmax → Target word prediction

### Components:
- **Vocabulary**: List of unique words in the corpus
- **Embedding Matrix (W)**: Transforms one-hot input vectors into dense vectors
- **Averaging Layer**: Combines embeddings of context words through averaging
- **Output Matrix (W')**: Transforms context vector into scores for all vocabulary words
- **Softmax**: Converts scores into probabilities
- **Loss Function**: Cross-entropy loss for training

## Implementation Process

The CBOW model is implemented through the following steps:

1. **Build Vocabulary**  
   Map each unique word to an index.

2. **One-hot Encode Context Words**  
   Convert each context word to a one-hot vector.

3. **Embedding Layer**  
   Multiply one-hot vectors with matrix `W` to get embeddings.

4. **Average Embeddings**  
   Combine context word embeddings using average.

5. **Output Layer**  
   Multiply the average vector with output matrix `W'` to get scores for all words.

6. **Softmax**  
   Convert scores to probabilities.

7. **Prediction & Training**  
   Use cross-entropy loss to compute error and update matrices `W` and `W'` using backpropagation.

## Example Walkthrough

Let's consider a simple example with the sentence: `"I love coding"`

We'll try to predict the target word `"love"` using the context: `["I", "coding"]`.

### Step-by-Step CBOW Process

#### 1. Vocabulary
Extract all unique words:
```
Vocabulary: ["I", "love", "coding"]
```

Assign indexes:
| Word    | Index |
|---------|-------|
| I       | 0     |
| love    | 1     |
| coding  | 2     |

Vocabulary size `V = 3`

#### 2. One-Hot Encoding for Context Words
Context words: `["I", "coding"]`
One-hot vectors (size = 3):
* "I" → [1, 0, 0]
* "coding" → [0, 0, 1]

#### 3. Embedding Matrix (W)
Assume **embedding size = 2**
Initialize `W` (shape `3 × 2`) randomly:
```
W = [
    [0.1, 0.2],  # "I"
    [0.0, 0.3],  # "love"
    [0.4, 0.5]   # "coding"
]
```

Use one-hot vectors to get embeddings:
* "I" → [0.1, 0.2]
* "coding" → [0.4, 0.5]

#### 4. Averaging Layer
Average context embeddings:
```
avg = ([0.1, 0.2] + [0.4, 0.5]) / 2 = [0.5, 0.7] / 2 = [0.25, 0.35]
```
This is the **context representation vector**.

#### 5. Output Matrix (W')
Define `W'` as `2 × 3` (embedding size × vocab size):
```
W' = [
    [0.2, 0.3, 0.5],  # Row 0
    [0.1, 0.4, 0.6]   # Row 1
]
```

Multiply `[0.25, 0.35]` with `W'`:
```
u = [0.25, 0.35] · W' = [score_I, score_love, score_coding]
```

Compute dot products:
* Score for "I": 0.25×0.2 + 0.35×0.1 = 0.05 + 0.035 = 0.085
* Score for "love": 0.25×0.3 + 0.35×0.4 = 0.075 + 0.14 = 0.215
* Score for "coding": 0.25×0.5 + 0.35×0.6 = 0.125 + 0.21 = 0.335

So, output scores = `[0.085, 0.215, 0.335]`

#### 6. Softmax Layer
Apply softmax: softmax(z_i) = e^(z_i) / ∑e^(z_j)

Exponentiate:
* exp(0.085) ≈ 1.0887
* exp(0.215) ≈ 1.2398
* exp(0.335) ≈ 1.3980

Sum = 1.0887 + 1.2398 + 1.3980 = **3.7265**

Probabilities:
* P("I") = 1.0887 / 3.7265 ≈ **0.292**
* P("love") = 1.2398 / 3.7265 ≈ **0.333**
* P("coding") = 1.3980 / 3.7265 ≈ **0.375**

#### 7. Loss Function (Cross-Entropy)
Actual target = **"love"**, which is index 1.
Cross-entropy loss: Loss = -log(P(true class)) = -log(0.333) ≈ 1.0986

## Applications

CBOW word embeddings can be used for various NLP tasks:
* Semantic similarity calculations
* Sentiment analysis
* Text classification
* Document clustering
* Machine translation
* Information retrieval

## Advantages and Limitations

### Advantages
* Fast to train compared to Skip-gram
* Works well with frequent words
* Uses less memory than other neural models
* Learns semantic meanings and relationships between words

### Limitations
* Ignores word order (since it uses bag of words internally)
* Not good for representing rare words
* Averages context (may lose nuanced meaning)
* Fixed window size limits context consideration
* Requires substantial training data for good results

## Code Implementation

### Usage
```python
# Example code for training a CBOW model
from cbow import CBOWModel

# Initialize model
model = CBOWModel(
    corpus_file="data/corpus.txt",  
    embedding_size=100,
    window_size=2
)

# Train the model
model.train(epochs=5)

# Get word embeddings
word_vectors = model.get_embeddings()

# Find similar words
similar_words = model.most_similar("coding", top_n=5)
```
