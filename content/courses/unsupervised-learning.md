+++
title = "Unsupervised Learning - Course Notes"
date = "2025-12-04"
author = "Max"
tags = ["machine learning", "unsupervised learning", "PCA", "K-means"]
description = "Key concepts and insights from unsupervised learning"
+++

## Overview

Unsupervised learning is **subjective**.

Unsupervised learning is useful during **Exploratory Data Analysis**.

requirements: linear algebra

---

## Two Main Tasks

### 1. Dimensionality Reduction
- Requires **centered data**
- Dimension `m` needs to be determined
- Example: Principal Component Analysis (PCA)

### 2. Clustering
- **Ill-posed problem** 
- Euclidean distance performs poorly in high dimensions
- Cluster number `k` needs to be determined
- Example: K-means clustering

---

## Principal Component Analysis (PCA)

### Key Terms

**Principal Components (PCs)**:
- First PC, Second PC, ...
- PC is a linear combination of loading vectors and data

**Loading Vectors**:
- The loadings are normalized
- Loading vectors are the slopes
- Indicate how much the current feature contributes to the PC

**Singular Value Decomposition (SVD)**:
- Formula: `X = USV^T`
- `U`: Left singular vectors (orthogonal matrix)
- `V`: Right singular vectors (orthogonal matrix)
- `S`: Diagonal matrix (singular values)

### Choosing Dimensions

You can choose the dimension you want to reduce to by selecting the number `m` in diagonal matrix `S`.

**Information loss** can be measured by matrix `S`:
- Total variance vs. Retained variance

---

## K-means Clustering

### Algorithm Approach

K-means uses an **iterative algorithm** instead of directly optimizing the mathematical target function (which is NP-hard).

### Determining K

K-means can use **heuristic approaches** to find a good cluster number `K`.

---

## Key Takeaways

- Unsupervised learning is subjective and exploratory
- PCA: Reduces dimensions while preserving variance
- K-means: Iterative clustering with predetermined K
- Both methods require parameter tuning (m for PCA, k for K-means)
