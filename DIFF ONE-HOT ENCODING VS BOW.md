# Comparing One-Hot Encoding and Bag of Words (BoW)

This README demonstrates the step-by-step implementation and comparison of two fundamental text representation techniques in Natural Language Processing (NLP): One-Hot Encoding and Bag of Words.

## Sample Text Used

```
"I love apple and I love banana"
```

## Assumptions

- All text is converted to lowercase
- Stopwords are not removed
- The vocabulary consists only of words in the sample text

## Step 1: Preprocessing

### Tokenization (after lowercasing)

```python
tokens = ["i", "love", "apple", "and", "i", "love", "banana"]
```

### Vocabulary Creation (sorted alphabetically)

```python
vocabulary = ["and", "apple", "banana", "i", "love"]
```

Vocabulary size = **5**

### Index Assignment

| Word   | Index |
|--------|-------|
| and    | 0     |
| apple  | 1     |
| banana | 2     |
| i      | 3     |
| love   | 4     |

## Step 2: One-Hot Encoding Implementation

In One-Hot Encoding, each word is represented by a binary vector where only one position contains 1 (corresponding to that word's index in the vocabulary), and all other positions contain 0.

### Word-to-Vector Mapping

| Word   | One-Hot Vector    |
|--------|-------------------|
| and    | [1, 0, 0, 0, 0]   |
| apple  | [0, 1, 0, 0, 0]   |
| banana | [0, 0, 1, 0, 0]   |
| i      | [0, 0, 0, 1, 0]   |
| love   | [0, 0, 0, 0, 1]   |

### Final Output for One-Hot Encoding

Each word in the sentence is represented individually:

```
"I"      → [0, 0, 0, 1, 0]
"love"   → [0, 0, 0, 0, 1]
"apple"  → [0, 1, 0, 0, 0]
"and"    → [1, 0, 0, 0, 0]
"I"      → [0, 0, 0, 1, 0]
"love"   → [0, 0, 0, 0, 1]
"banana" → [0, 0, 1, 0, 0]
```

**Important Note**: One-Hot Encoding preserves the original sequence of words but does not capture information about word frequency or sentence structure. Each word instance gets its own vector regardless of how many times it appears.

## Step 3: Bag of Words (BoW) Implementation

Bag of Words counts how many times each word appears in the document (in this case, our sentence).

### Word Frequency Counting

| Word   | Count |
|--------|-------|
| and    | 1     |
| apple  | 1     |
| banana | 1     |
| i      | 2     |
| love   | 2     |

### BoW Vector Creation

```
[1, 1, 1, 2, 2]  # [and, apple, banana, i, love]
```

### Final Output for Bag of Words

The entire sentence is represented by a single vector:

```
"I love apple and I love banana" → [1, 1, 1, 2, 2]
```

This tells us:
- "i" appears 2 times
- "love" appears 2 times
- "and", "apple", and "banana" each appear once

## Comparison: One-Hot Encoding vs. Bag of Words

| Feature | One-Hot Encoding | Bag of Words |
|---------|------------------|--------------|
| Output | One vector **per word** | One vector **per sentence/document** |
| Example | "love" → `[0, 0, 0, 0, 1]` | Entire sentence → `[1, 1, 1, 2, 2]` |
| Frequency captured? | ❌ No | ✅ Yes |
| Word order preserved? | ✅ Yes (as separate vectors) | ❌ No |
| Semantic/context info | ❌ No | ❌ No |
| Vector sparsity | Higher (mostly zeros) | Lower (counts) |
| Vector size | Same as vocabulary size | Same as vocabulary size |
| Use case | Individual word representation | Document classification |

## Visual Representation

### One-Hot Encoding (Matrix Form)
Each row represents a token in the sentence:

```
Token 1 (i):      [0, 0, 0, 1, 0]
Token 2 (love):   [0, 0, 0, 0, 1]
Token 3 (apple):  [0, 1, 0, 0, 0]
Token 4 (and):    [1, 0, 0, 0, 0]
Token 5 (i):      [0, 0, 0, 1, 0]
Token 6 (love):   [0, 0, 0, 0, 1]
Token 7 (banana): [0, 0, 1, 0, 0]
```

### Bag of Words (Vector Form)
One single vector for the entire sentence:

```
[1, 1, 1, 2, 2]
```


## Use Cases

### One-Hot Encoding
- Input for word embeddings (like Word2Vec)
- Neural network input where sequential information is needed
- Preprocessing step for more advanced NLP techniques

### Bag of Words
- Document classification
- Information retrieval
- Feature extraction for machine learning models
- Topic modeling

## Limitations

Both techniques fail to capture semantic relationships between words. More advanced techniques like word embeddings (Word2Vec, GloVe) and contextual embeddings (BERT, GPT) address these limitations by learning dense vector representations that encode semantic meaning.
