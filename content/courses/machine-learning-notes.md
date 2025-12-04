machine learning and statistical modeling
Model Interpretability: easy model == good interpretability

applied machine learning:
1. regression 
2. classification

frequentist: beta is fixed with some noise.
1. linear model (LM)
model formula: y = beta1x1 + beta2x2 + error(based on Gaussian distribution)
optimization method: OLS (Ordinary Least Squares)
performance metrics: MAE, RMSE, MSE
2. generalized linear model (GLM)
model formula: event probability mu = f(x, beta), y = 0 if mu < thresh elif y = 1 if mu >= tresh
threshold: matter a lot. ROC, AUC
confusion matrix: TP, TN, FP, FN
ROC: x:False positive rate, y: TPR, recall; it is a curve
AUC: area under the ROC curve
important terms: decision making, event probability, accuracy, ROC, AUC, threshold, confusion matrix, event/non-event
performance metrics: Cross-Entropy (binary: log loss; multi-class: softmax loss)

bayesian: beta is a random variable
- distribution fitting (*Gaussian)
    - conjugate prior(closed/analytical solution)
    - laplace approximation
1. bayesian linear model (BLM)
model formula: posterior = prior(knowledge) + likelihood(data, purely frequentist)
unique performance metrics: bayes factor(comparison), model evidence(alone)
some math terms: derivative, closed solution, taylor expansion, order

2. bayesian logistic regression

feature selection:
1. additive feature
2. interaction

regularization:
1. LM: Lasso(L1), Ridge(L2) 
2. BLM: prior

insights:
1. Neural network we don't care about preditive behavior because it is too complex to explain. But as for ML, model is simple and you can clearly see how the features interact with the output, and the preditive behavior (like the uncertainty interval of certain feature) is pretty obvious.
2. Acc vs. AUC: Acc highly relies on threshold. AUC doesn't. For binary classification case, some times the dataset is imbalanced, which means it may have a log of events but a few of non-events. In this case, if small set of non-events are false, the Acc is good but AUC is bad (because False positve rate is low, no matter recall is high, it doesn't matter, we need low FPR and high recall so that we are confident about the model). It's a thing about data balance in classification, and the different between regression and classification.
*3. Laplace approximation: The mathematical form of the second-order Taylor expansion around the Maximum Likelihood Estimate (MLE) is the Gaussian distribution, given that the first derivative is zero. This principle is the foundation of the locally accurate Laplace approximation.
4. OLS's result == MLE's result
5. credible interval vs. confidence interval: Bayesian vs. frequentist
    - credible interval: the parameter is 95% probability inside the interval
    - confidence interval: if we did experiments 100 times, 95 times the parameter will be inside the interval
    *similar but different explanation.