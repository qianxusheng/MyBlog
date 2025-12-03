+++
title = "Information Storage and Retrieval - Course Notes"
date = "2025-11-30"
author = "Max"
tags = ["course", "information retrieval", "machine learning"]
description = "My notes and insights from the Information Storage and Retrieval course (Tech stack: Java -> Luence -> Elasticsearch)"
+++
## Part I: Core Concepts & My Insights

### 1. Terminology: Token vs Term
- **Token**: Word after tokenization (raw unit from text splitting)
- **Term**: Token after stemming and normalization (standardized unit for indexing)

---

### 2. Evolution of IR: Traditional vs Modern

| Aspect | Traditional IR | Modern IR (Semantic Retrieval) |
|--------|---------------|-------------------------------|
| **Vector Type** | Sparse vectors | Dense vectors |
| **Matching** | Lexical matching | Semantic matching |
| **Basis** | Term-based | Context-based |
| **Examples** | TF-IDF, BM25 | BERT, Transformers |

---

### 3. N-gram: Context Capture but NOT Semantic Retrieval

**N-gram approach**: Treats n consecutive words as a single "term"
- Captures local context and word order relationship
- As n increases → more context captured

**But it's still lexical matching, NOT semantic!**
- ❌ Cannot match synonyms: "car" ≠ "automobile"
- ❌ Cannot match paraphrases: "New York University" ≠ "NYU"
- ✅ BERT-based modern IR can do these!

**My insight**: N-gram improves traditional IR by preserving phrases, but it's fundamentally different from semantic retrieval.

---

### 4. Index Compression

**Problem**: Posting lists can be huge (millions of docIDs) → hundreds of GB storage

**Solution - Two-step approach**:

#### Step 1: Gap Encoding (d-gap)
- Store **differences** between adjacent docIDs, not absolute values
- Example: [5, 23, 45, 89] → [5, 18, 22, 44]
- Result: Large numbers → Small numbers

#### Step 2: Variable-Length Encoding
Choose one:

**a) Gamma Encoding** (Elias Gamma Code):
- Small numbers use fewer bits
- Example: 5 → 00101 (5 bits), 1 → 1 (1 bit)
- Best compression ratio

**b) Delta Encoding** (Elias Delta Code):
- Improvement over Gamma for larger numbers

**c) VByte Encoding**:
- Byte-aligned (faster decoding)
- Commonly used in practice (Lucene, Elasticsearch)

**Result**: 5-10× compression (100 GB → 10-20 GB)

**My insight**: Gap + Gamma is the classic combo - transform data first, then compress efficiently!

---

### 5. Retrieval Models: Boolean vs Best Match

**Boolean Model**:
- Exact match (AND/OR/NOT logic)
- Returns unranked set
- Binary relevance (relevant or not)

**Best Match Model (BM)**:
- Partial match
- Returns ranked list ordered by relevance scores
- Graded relevance (score 0-1)
- **BM25** is a specific implementation

---

### 6. TF-IDF and BM25: Core Ranking Algorithms

**TF-IDF**:
- **TF (Term Frequency)**: count(t, D) / |D|
  (how often term appears in document)
- **IDF (Inverse Document Frequency)**: log(N / df_t)
  (how rare the term is across all documents)
- **Score**: TF × IDF (term weight for ranking)

**BM25**:
- Improved version of TF-IDF
- Addresses TF-IDF's issues:
  1. Term frequency saturation (non-linear growth)
  2. Better document length normalization
  3. Tunable parameters (k1, b)
- **Modern search engines' default choice** (Elasticsearch, Lucene)

---

### 7. Traditional IR Models: VSM vs Language Model

**Vector Space Model (VSM)**:
- Construct query and document vectors using TF-IDF weights
- Compute **cosine similarity** for ranking
- Geometric approach (vectors in high-dimensional space)

**Statistical Language Model (LM)**:
- **Query Likelihood**: P(Q|D) = Π P(q_i|D)
- **Dirichlet Smoothing**: Handle zero probability problem
- Probabilistic approach

**Key insight**: Both are sparse vector methods, but different mathematical frameworks.

---

### 8. Log Probability: Numerical Stability

**Why use log?**
- Direct probability multiplication: P(q1|D) × P(q2|D) × ... → underflow!
- Log transform: log P(Q|D) = Σ log P(qi|D) (multiplication → addition)
- **Prevents underflow** when computing many small probabilities

---

### 9. Smoothing: Solving Zero Probability Problem

**Problem**:
- Query term not in document → P(t|D) = 0 → entire score = 0!

**Solution - Smoothing**:
- Mix document probability with collection probability
- Assigns non-zero probabilities to unseen terms
- **Most common**: Dirichlet Smoothing with μ ≈ 2000

**Formula**: P_smooth(t|D) = (count(t,D) + μ × P(t|C)) / (|D| + μ)

**My insight**: Smoothing not only solves zero probability but also provides automatic document length normalization.

---

### 10. TF-IDF's Origin

**Interesting connection**: The idea of TF-IDF originally comes from statistical language models, but we commonly use it in VSM framework.

---

### 11. Query Feedback and Query Expansion

**Problem**: Short queries → vocabulary mismatch → poor retrieval

#### Query Feedback Types:

**Explicit Feedback**:
- User actively provides signals: clicking, rating, bookmarking

**Implicit Feedback**:
- System automatically collects: mouse hover time, scroll depth, dwell time

#### Query Expansion Approaches:

**1. Relevance Feedback**:
- User marks relevant docs → extract terms → expand query

**2. Pseudo Relevance Feedback (PRF)**:
- **Assume top-k results are relevant** (no user input!)
- Extract terms from top-k docs
- Expand query automatically
- Example: "jaguar" → top-3 about animals → extract "wild, hunting, cats" → "jaguar wild hunting cats"

**3. Implicit Feedback**:
- Use user behavior signals to expand query

**My insight**: PRF is brilliant for disambiguation without user effort!

---

### 12. Evaluation Metrics

**Key metrics evolution**:
- AP (Average Precision) → MAP (Mean AP) → DCG → **NDCG**
- **NDCG** (Normalized Discounted Cumulative Gain) is most important

**My take**: Not my primary interest area, but essential for comparing IR systems. Requires labeled datasets like ML tasks.

---

### 13. Learning to Rank (LTR): ML + IR

**Core idea**:
- Use machine learning to optimize ranking
- **Different from** regression/classification → output is a ranked list

**Three approaches**:
1. **Pointwise**: Predict relevance score for each document
2. **Pairwise**: Learn relative ordering between document pairs (RankNet, LambdaMART)
3. **Listwise**: Directly optimize entire ranked list (ListNet, AdaRank)

**Key insight**:
- **NOT replacing** traditional methods
- **Combining** multiple signals as features:
  - Content features: BM25, TF-IDF, LM scores
  - Quality features: PageRank, domain authority
  - User features: CTR, dwell time
- ML model learns optimal combination

**Typical pipeline**:
1. Initial retrieval: BM25 gets top-1000
2. Feature extraction: ~50-200 features per query-doc pair
3. ML model predicts final scores
4. Re-ranking by ML scores
5. Return top-10

---

### 14. Neural IR Models: BERT-based Dense Retrieval

**Foundation**: BERT (Transformer-based encoder)
- Produces dense vectors (e.g., 384-dim)
- Captures semantic meaning

#### Dual-Encoder Architecture
- **Two separate encoders**: one for documents, one for queries
- **Offline**: Preprocess entire corpus into vectors, store in vector DB
- **Online**: Encode query in real-time, compute similarity (cosine/dot product)
- **Pros**: Fast, scalable
- **Cons**: Lower accuracy (no query-document interaction)

#### Cross-Encoder Architecture
- **Single joint encoder**: [Query, Document] → Relevance Score
- **Online**: For each query-doc pair, concatenate and feed to BERT
- **Interaction**: Query and document tokens attend to each other via attention mechanism
- **Pros**: High accuracy (full token-level interaction)
- **Cons**: Slow, not scalable (cannot precompute)

**Why interaction works better?**
- Dual-Encoder: Only overall vector similarity (coarse-grained)
- Cross-Encoder: Token-to-token attention (fine-grained)
  - "recipe" (Q) attends to "bake" (D) → semantic match
  - Captures word order, negations, partial matches

#### Best Practice: Two-Stage Retrieval
1. **Stage 1 (Recall)**: Dual-Encoder retrieves top-100 from millions
2. **Stage 2 (Re-rank)**: Cross-Encoder re-ranks top-100 → top-10

**Example pipeline**: BM25 → Dual-Encoder → Cross-Encoder

---

## Part II: Course Assignments

### Assignment 1: TREC Corpus Preprocessing

**Task**: Build a preprocessing pipeline for the TREC corpus (traditional IR benchmark dataset)

**Technologies**: Java

**Pipeline components**:
1. **Tokenization**: Split text into tokens
2. **Normalization**: Convert to lowercase, handle punctuation
3. **Stopword Removal**: Remove meaningless words like "and", "the", "of"
4. **Stemming**: Reduce words to root form (e.g., "running" → "run")

**What I learned**:
- Hands-on experience with traditional IR preprocessing
- Understanding the importance of each step in the pipeline
- Java implementation of text processing

---

### Assignment 2: Building Inverted Index with External Merge

**Task**: Implement a scalable inverted index builder for large corpus

**Key components**:

**1. Inverted Index Structure**:
- **Vocabulary List**: Terms and their document frequencies
- **Posting List**: For each term → list of (docID, term frequency) pairs

**2. Scalability Challenge**:
- Corpus too large to fit in memory
- Need efficient I/O streaming pipeline

**3. Solution: External K-Way Merge**:

**Block-based Indexing**:
```
Step 1: Index in blocks
  - Read a block of documents (fits in memory)
  - Build in-memory index using TreeMap (keeps terms sorted)
  - Write block index to disk
  - Repeat for all blocks

Step 2: External merge
  - K pointers to K posting files on disk
  - Read one posting entry from each file into memory
  - Merge postings with same term (since sorted by TreeMap)
  - Write merged posting to final index
```

**What I learned**:
- External sorting/merging algorithms for handling large-scale data
- I/O optimization for disk-based indexing
- TreeMap ensures sorted order → enables efficient merging

---

### Assignment 3: Query Likelihood Model with Lucene

**Task**: Implement statistical language model using Lucene

**Technologies**: Lucene API

**Model implementation**:
- **Language Model**: Query Likelihood with Dirichlet Smoothing
- **Formula**: P_smooth(t|D) = (count(t,D) + μ × P(t|C)) / (|D| + μ)
- **Parameter**: μ ≈ 2000 (typical value)

**Key challenges handled**:

**1. Zero probability problem**:
- Handled by Dirichlet smoothing (terms in document but low frequency)

**2. Unseen terms in entire corpus**:
- Terms not in vocabulary at all
- Assigned small baseline probability to prevent complete failure

**What I learned**:
- Practical implementation of probabilistic IR models
- Lucene API for custom scoring
- Importance of smoothing in real systems

---

### Assignment 4: Pseudo Relevance Feedback

**Task**: Enhance retrieval with PRF on top of Query Likelihood Model

**Based on**: Assignment 3 (Query Likelihood + Dirichlet Smoothing)

**Two-stage retrieval approach**:

**Stage 1: Initial Retrieval**:
- Use original query Q
- Retrieve top-N documents (e.g., N=10)
- Assume these are relevant (pseudo feedback)

**Stage 2: Query Expansion & Re-ranking**:
```
1. Extract terms from top-N docs
2. Treat top-N docs as a "mini corpus"
3. Calculate new term probabilities: P(t|pseudo_corpus)
4. Expand original query with high-scoring terms
5. Re-score all documents with expanded query
```

**Final scoring**:
```
Score_final = λ × Score_original + (1-λ) × Score_PRF

where:
- Score_original: Original query likelihood score
- Score_PRF: Score based on expanded query from PRF
- λ: Mixing parameter (e.g., 0.7)
```

**What I learned**:
- Two-stage retrieval pipeline (recall → re-rank)
- Query expansion without explicit user feedback
- How PRF can improve retrieval for ambiguous queries
- Trade-off: Better accuracy but slower (need two passes)

---

### Final Project: Legal Retrieval System

**Task**: Build a production-ready legal document retrieval system

**Technologies**:
- **Elasticsearch**: Industrial-grade search engine
- **Legal BERT**: Domain-specific semantic encoder
- **Dual-Encoder**: Fast recall from large corpus
- **Cross-Encoder**: Accurate re-ranking

**Architecture**:
We utilized Elasticsearch to build a legal retrieval system, using Legal BERT as the semantic vector encoder with dual-encoder for recall and cross-encoder for re-ranking.

---

## Part III: Summary

### IR System Pipeline Evolution
```
  → Corpus Preprocessing (stemming...)
  → Indexing (index compression)
  → Model (ranking algorithm)
  → Evaluation (Precision, NDCG)
  → Feedback and Query Expansion (PRF)
  → LTR (VSM/LM + feature selection + pairwise + ML)
  → Neural IR (BERT)
```

### Key Takeaways

**1. Query Enhancement**:
Short queries can lead to poor retrieval, so we can enhance the query through explicit, implicit, or pseudo feedback.

**2. Course Journey**:
This class taught us how to build a traditional IR system from scratch. We learned how to preprocess and index the corpus in Java, then learned how to use Lucene to help us speed up indexing and create a query likelihood model, which we improved by adding PRF. In the final project, we used Elasticsearch, an industrial-grade search engine. Although we haven't used the industrial-level features of Elasticsearch, it was still good to know this search engine, and it may be helpful in the future. I also played with BERT quite a bit and learned how to build dense vector models.