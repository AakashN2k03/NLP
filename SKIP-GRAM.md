# Skip-Gram Model

Skip-Gram Model – a variant of Word2Vec that learns word embeddings by predicting surrounding context words from a single target word.

## 🧠 Overview
Skip-gram is a shallow neural network used in NLP that aims to learn word embeddings by predicting context words based on a center (target) word.

Unlike CBOW (which predicts target word from context), Skip-gram works in reverse:

Given: "coding"
Predict: context → "love", "everyday"

The learned embeddings capture semantic relationships — words used in similar contexts get similar vectors.

## ❓ What is Skip-gram?
Skip-gram learns to predict context words given a target word.

🧾 **Example:**
- Sentence: "I love coding everyday"
- Target word: "coding"
- Context (window=1): ["love", "everyday"]

Skip-gram learns to:
- "coding" → "love"
- "coding" → "everyday"

This results in word vectors that preserve semantic similarity and analogy structure.

## 🧱 Architecture
```
Target Word → One-Hot Encoding → Embedding Matrix (W1) → Dense Vector →
→ Output Matrix (W2) → Scores for all words → Softmax → Predict context words
```

**Components:**
| Component | Role |
|-----------|------|
| Vocabulary | Unique words in corpus |
| Embedding Matrix (W1) | Transforms target one-hot into dense vector |
| Output Matrix (W2) | Transforms dense vector into scores for all vocab words |
| Softmax | Converts raw scores to probabilities |
| Loss Function | Cross-entropy, summed over each context prediction |

## 🛠 Implementation Process
1. **Build Vocabulary**
   Assign each unique word an index.

2. **One-hot Encode Target Word**
   Convert target word to one-hot vector.

3. **Embedding Layer (W1)**
   Multiply one-hot vector with W1 to get dense vector.

4. **Output Layer (W2)**
   Multiply dense vector with W2 to get raw scores.

5. **Softmax**
   Convert scores to probabilities.

6. **Prediction & Training**
   For each context word: compute loss and update W1, W2 using backpropagation.

## 🔁 Example Walkthrough
Let's predict the context words for:
- Sentence: "I love coding"
- Target word: "love"
- Context (window size = 1): ["I", "coding"]

### 1. Vocabulary
```
Vocabulary: ["I", "love", "coding"]
Indexes: {"I": 0, "love": 1, "coding": 2}
Vocabulary size V = 3
```

### 2. One-hot Encode Target Word: "love"
One-hot:
```
[0, 1, 0]  ← one-hot for "love"
```

### 3. Embedding Matrix W1
Let embedding dimension = 2
Randomly initialize W1 (3 × 2):
```python
W1 = [
    [0.1, 0.2],  # "I"
    [0.3, 0.5],  # "love"
    [0.6, 0.1]   # "coding"
]
```
One-hot vector × W1 = [0, 1, 0] × W1 = [0.3, 0.5]
This is the dense embedding for "love"

### 4. Output Matrix W2
W2 = (2 × 3) matrix (since output layer maps embedding to vocab size)
```python
W2 = [
    [0.4, 0.1, 0.6],
    [0.2, 0.5, 0.3]
]
```
Now compute:
```
[0.3, 0.5] × W2 = scores for all words
```
Dot products:
```
score("I")      = 0.3×0.4 + 0.5×0.2 = 0.12 + 0.10 = 0.22  
score("love")   = 0.3×0.1 + 0.5×0.5 = 0.03 + 0.25 = 0.28  
score("coding") = 0.3×0.6 + 0.5×0.3 = 0.18 + 0.15 = 0.33
```

### 5. Softmax
Exponentiate:
```
exp(0.22) ≈ 1.246  
exp(0.28) ≈ 1.323  
exp(0.33) ≈ 1.391
```
Sum = 3.96

Probabilities:
```
P("I")      = 1.246 / 3.96 ≈ 0.315  
P("love")   = 1.323 / 3.96 ≈ 0.334  
P("coding") = 1.391 / 3.96 ≈ 0.351
```

### 6. Cross-Entropy Loss (for each context word)
For context = ["I", "coding"]
- Actual labels: [1, 0, 0] for "I", [0, 0, 1] for "coding"
- Predicted probabilities: as above

Loss = -log(P("I")) + -log(P("coding"))
= -log(0.315) + -log(0.351) ≈ 1.154 + 1.046 = 2.2

### 7. Backpropagation
- Gradients are computed for both W1 and W2
- Update the parameters to minimize the loss

## 🎯 Applications
- Semantic similarity
- Text classification
- Named Entity Recognition
- Text generation

## ✅ Advantages and 🚫 Limitations

| ✅ Advantages | 🚫 Limitations |
|---------------|----------------|
| Works well for rare words | Slower than CBOW (predicts multiple words) |
| Captures rich word relationships | Needs more training data |
| Good at capturing semantics | More memory usage than CBOW |
| Can use negative sampling | Ignores word order |

## Code Implementation

### Usage
```python
# Example code for training a CBOW model
# main.py
from skipgram import SkipGramModel

# Initialize model
model = SkipGramModel(
    corpus_file="data/corpus.txt",
    embedding_size=50,
    window_size=2
)

# Train model
model.train(epochs=10, lr=0.05)

# Get embeddings
word_vectors = model.get_embeddings()

# Find similar words
similar = model.most_similar("coding", top_n=5)
print("Most similar to 'coding':", similar)

```


## 🔚 Summary Comparison: CBOW vs Skip-gram

| Aspect | CBOW | Skip-gram |
|--------|------|-----------|
| Input | Context words | Target word |
| Output | Predict center word | Predict context words |
| Training speed | Faster | Slower |
| Rare words | Poorly represented | Well represented |
| Use case | High frequency word modeling | Richer semantic capture |
