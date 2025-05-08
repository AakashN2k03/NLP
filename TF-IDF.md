# 📚 TF-IDF (Term Frequency–Inverse Document Frequency)
TF-IDF is a statistical measure used in **text mining** and **information retrieval** to evaluate how important a word is to a **document** in a **corpus**.
---
## 📌 What is TF-IDF?
**TF-IDF** helps highlight words that are more **informative** and **unique** to a document, while reducing the weight of **common words** (like "the", "is", "and").
**Formula**:
## TF-IDF = TF * IDF
---
## 🔸 Term Frequency (TF)
TF measures how often a term occurs in a document.
## TF= ( NO OF REPETITION OF WORDS IN A SENTENCE / NO OF WORDS IN A SENETENCE)
**Example**:  
### EG : GOOD BOY
- TF for word boy = 1/2
---
## 🔸 Inverse Document Frequency (IDF)
IDF measures how **unique** or **rare** a term is across all documents in the corpus.
## IDF =LOG( NO OF SENTENCES/ NO OF SENTENCES CONTAINING THE WORD)
**Example**:  
- sentence 1 : good boy
- sentence 2: good girl
- IDF for the word good = log(2/2)=0
---
## 🔹 TF-IDF Example
 - CALCULATE TF AND IDF FOR EACH SENTENCES AND MULTIPLY CORRESPONDINGLY ### (TF*IDF)
This means "boy" has moderate importance in the first sentence.
---
## 📘 Example Corpus
3 Documents:
1. "the cat sat on the mat"  
2. "the dog sat on the log"  
3. "the cat chased the dog"
To compute TF-IDF for "cat" in Document 1:
- `TF = 1/6 = 0.166`
- Appears in 2 of 3 docs → `df("cat") = 2`
- `IDF = log(3 / (1+2)) = log(1) = 0`  
→ `TF-IDF = 0.166 × 0 = 0`
---
## 🧾 Definitions
- **Document**: A single piece of text (e.g., one article, review).
- **Corpus**: A collection of documents.
---
## ✅ Advantages
- Simple and fast to compute  
- Filters out common words  
- Highlights important words per document  
---
## ❌ Limitations
- No understanding of **context** or **semantics**  
- Treats synonyms as different (e.g., "car" ≠ "automobile")  
- Sensitive to spelling and word forms  
---
## 🧠 Semantic Limitation Explained
TF-IDF treats:
- "car" and "automobile" → as different words  
- "run" and "running" → as unrelated  
- "bank" (money) and "bank" (river) → same, without context
It lacks semantic understanding.
---
## 📦 Alternatives
For capturing **meaning/context**, consider:
- Word Embeddings: Word2Vec, GloVe  
- Contextual Models: BERT, GPT, etc.
---
## 🔗 Applications
- Document similarity (cosine similarity on TF-IDF vectors)
- Text classification
- Search engines
- Keyword extraction
---
## 🛠 Libraries in Python
```python
from sklearn.feature_extraction.text import TfidfVectorizer
corpus = ["the cat sat on the mat", "the dog sat on the log"]
vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(corpus)
