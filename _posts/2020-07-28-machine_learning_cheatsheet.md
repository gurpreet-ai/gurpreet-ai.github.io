---
layout: post
title:  "Machine Learning Cheatsheet"
date:   2020-07-28 12:00:00
---


## Goal

The goal of this cheatsheet is to briefly summarize machine learning algorithms, advantages, and use cases. I want to reference the original Machine Learning Cheatsheet written by Remi Canard. Thank you Remi.

## Topics

 - General
	 - Definition of Machine Learning
	 - Linear vs Non-linear Algorithms
	 - Supervised vs Unsupervised Learning
	 - Bias-Variance trade-off
	 - Underfitting and Overfitting
- Optimization
	- Gradient Descent

## General

**Definition**

We want to learn a target function $$f$$ that maps input variable $$X$$ to output variable $$Y$$, with an error $$e$$:

$$Y = f(X) + e$$

**Linear vs Non-linear Algorithms**

Any algorithm can be linear (or parametric) or non-linear (or non-parametric). Linear algorithms are usually simpler, faster, and require less data whereas non-linear algorithm are more flexible, more powerful (they can represent a larger class of functions), and more performant but much harder to train.

 - **Linear (or parametric)**: simplify the mapping to a known linear combination form and learning its coefficients
 - **Non-linear (or non-parametric)**: free to learn any functional form from the training data, while maintaining some ability to generalize.

**Supervised vs Unsupervised Learning**

- **Supervised learning** methods learn to predict Y from X given that the data is labeled.
- **Unsupervised learning** methods learn	to find the inherent structure of the unlabeled data.

![enter image description here](https://4.bp.blogspot.com/-mC4Sn0NKt0k/XyBRb-5PUYI/AAAAAAAAJpY/c2p7dv0k3CUprTpu73oDYl6G12QsZAIHACLcBGAsYHQ/s1600/supervised.jpg)

**Bias-Variance trade-off**

In supervised learning, the prediction error $$e$$ is composed of the bias, the variance, and the irreducible part.

 - **Bias** refers to simplifying assumptions made to learn the target function easily.
 - **Variance** refers to sensitivity of the model to changes in the training data.

The **goal of parametrization** (writing in terms of parameters) is to achieve a **low bias** (underlying pattern not too simplified), and **low variance** (not sensitive to the specificities of the training data) tradeoff.

![enter image description here](https://2.bp.blogspot.com/-8GWIPcEkU80/XyBOoLOQJ_I/AAAAAAAAJpE/YafFZIJlNbo-Bsm2CvMbGYyofdgGKA3WgCLcBGAsYHQ/s1600/bias-variance.png)

**Underfitting and Overfitting**

In statistics, fit refers to how well the target function is approximated. 

 - **Underfitting** refers to poor inductive learning from training data and poor generalization.
 - **Overfitting** refers to learning the training data detail and noise which leads to poor generalization. It can be limited by using resampling, and defining a validation dataset.

Dealing with bias and variance is really about dealing with over and under-fitting. Bias is reduced and variance is increased in relation to model complexity. As more and more parameters are added to a model, the complexity of the model rises and variance becomes our primary concern while bias steadily falls.

![enter image description here](https://4.bp.blogspot.com/-_nEqJwioHF4/XyBRBL2nkeI/AAAAAAAAJpQ/2wOenkV7SLc8r8MY5-fuWJiB-GHlDt_OwCLcBGAsYHQ/s1600/Screen+Shot+2020-07-28+at+12.19.23+PM.png)

The sweet spot for any model is the level of complexity at which the increase in bias is equivalent to the reduction in variance. If our model complexity exceeds this sweet spot, we are in effect over-fitting our model; while if our complexity falls short of the sweet spot, we are under-fitting the model.

## Optimization

Optimization refers to the task of minimizing/maximizing an objective function $$f(x)$$ parameterized by $$x$$. In machine learning, it’s the task of minimizing the cost or loss function $$J(\theta)$$ parameterized by the model’s parameters $$\theta \in R^d$$. In the case of minimization, **optimization have one of the following goals**:

 - Find the global minimum of the objective function. This is feasible if the objective function is **convex**, i.e. any local minimum is a global minimum.
 - Find the lowest possible value of the objective function within its neighborhood. That’s usually the case if the objective function is **not convex** as the case in most deep learning problems.

**Gradient Descent**

Gradient Descent is the most common optimization algorithm. It is a first-order optimization algorithm meaning it takes into account the first derivative when performing the updates on the parameters. On each iteration, we update the parameters in the opposite direction of the gradient of the objective function $$\triangledown_\theta J(\theta)$$ w.r.t the parameters where the gradient gives the direction of the steepest ascent. The size of the step we take on each iteration to reach the local minimum is determined by the learning rate $$\alpha$$. Therefore, we follow the direction of the slope downhill until we reach a local minimum. In other words, we follow the direction of the slope of the surface created by the objective function downhill until we reach a valley.

*Algorithm*

- Initialization coefficients $$\theta = 0$$ or random value
- Pick a value for the learning rate $$\alpha$$. If $$\alpha$$ is very small, it would take long time to converge and become computationally expensive. If $$\alpha$$ is large, it may fail to converge and overshoot the minimum. The most commonly used rates are : $$0.001, 0.003, 0.01, 0.03, 0.1, 0.3$$.
- 
- Calculate cost: $$J(\theta)=evaluate(f(coefficients))$$
- Gradient of the cost: $$\frac{\delta}{\delta\theta_J}J(\theta)$$
- Update coefficients: $$\theta_j =\theta_j - \alpha \frac{\delta}{\delta\theta_J}J(\theta)$$

The cost updating process is repeated until convergence or until minimum is found.

**Ordinary Least Squares**

**Maximum Likelihood Estimation**


## Linear Algorithms

All linear algorithms assume a linear relationship between the input variables $$X$$ and the output variable $$Y$$.

**Linear Regression**

**Logistic Regression**

**PCA**

**LDA**

## Non-Linear Algorithms

**Classification and Regression Trees**

**Naive Bayes Classifier**

**K-Nearest Neighbors**

**SVM**

## Ensemble Algorithms

**Bagging and Random Forest**

**Boosting and AdaBoost**

