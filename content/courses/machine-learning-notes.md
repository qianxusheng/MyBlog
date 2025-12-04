+++
title = "Machine Learning and Statistical Modeling - Course Notes"
date = "2025-12-03"
author = "Max"
tags = ["machine learning", "statistical modeling", "bayesian", "regression", "classification"]
description = "Notes covering linear models, GLM, Bayesian approaches, and key ML concepts"
+++

## Overview

**Machine learning and statistical modeling**

**Model Interpretability**: easy model == good interpretability

---

## Applied Machine Learning

1. regression
2. classification

---

## Frequentist Approach

**Assumption**: beta is fixed with some noise.

### 1. Linear Model (LM)

**Model formula**: y = beta1x1 + beta2x2 + error(based on Gaussian distribution)

**Optimization method**: OLS (Ordinary Least Squares)

**Performance metrics**: MAE, RMSE, MSE

### 2. Generalized Linear Model (GLM)

**Model formula**: event probability mu = f(x, beta), y = 0 if mu < thresh elif y = 1 if mu >= tresh

**Threshold**: matter a lot. ROC, AUC

**Confusion matrix**: TP, TN, FP, FN

**ROC**: x:False positive rate, y: TPR, recall; it is a curve

**AUC**: area under the ROC curve

**Important terms**: decision making, event probability, accuracy, ROC, AUC, threshold, confusion matrix, event/non-event

**Performance metrics**: Cross-Entropy (binary: log loss; multi-class: softmax loss)

---

## Bayesian Approach

**Assumption**: beta is a random variable

**Distribution fitting** (*Gaussian):
- conjugate prior(closed/analytical solution)
- laplace approximation

### 1. Bayesian Linear Model (BLM)

**Model formula**: posterior = prior(knowledge) + likelihood(data, purely frequentist)

**Unique performance metrics**: bayes factor(comparison), model evidence(alone), AIC/BIC(penalty on complicated model. BIC's penalty is stricter)

**Some math terms**: derivative, closed solution, taylor expansion, order

### 2. Bayesian Logistic Regression
link function: e.g. logittic function
Convert linear preditor to event probability.

---

## Feature Selection

1. additive feature
2. interactive feature
3. n-degree of freedom spline feature(based on Polynomial Basis)

We can process categorical variables into numerical variables by adding dummy variables (one-hot coding).

---

## Linear vs Non-linear Models

Linear model has closed solution, easy computation and clear statistical analysis. non-linear model needs iterative optimization like gradient descendent.

Linear model means the unknown coefficients are linearly related to the mean trend.

---

## Regularization

1. **LM**: Lasso(L1), Ridge(L2)
2. **BLM**: prior

---

## Insights

### 1. Neural Network vs ML
Neural network we don't care about preditive behavior because it is too complex to explain. But as for ML, model is simple and you can clearly see how the features interact with the output, and the preditive behavior (like the uncertainty interval of certain feature) is pretty obvious.

### 2. Acc vs. AUC
Acc highly relies on threshold. AUC doesn't. For binary classification case, some times the dataset is imbalanced, which means it may have a log of events but a few of non-events. In this case, if small set of non-events are false, the Acc is good but AUC is bad (because False positve rate is low, no matter recall is high, it doesn't matter, we need low FPR and high recall so that we are confident about the model). It's a thing about data balance in classification, and the different between regression and classification.

### 3. Laplace Approximation
*Laplace approximation: The mathematical form of the second-order Taylor expansion around the Maximum Likelihood Estimate (MLE) is the Gaussian distribution, given that the first derivative is zero. This principle is the foundation of the locally accurate Laplace approximation.

### 4. OLS vs MLE
OLS's result == MLE's result

### 5. Credible Interval vs. Confidence Interval
Bayesian vs. frequentist
- **credible interval**: the parameter is 95% probability inside the interval
- **confidence interval**: if we did experiments 100 times, 95 times the parameter will be inside the interval

*similar but different explanation.
