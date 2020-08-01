---
layout: post
title:  "Machine Learning Engineer Cheatsheet"
date:   2020-07-28 12:00:00
---


## Goal

The goal of this cheatsheet is to briefly summarize machine learning concepts and algorithms. Thank you to the following sources:
- Data Science Cheatsheet Compiled by Maverick Lin
- Machine Learning Cheatsheet by Rémi Canard.
- Super VIP Cheatsheet: Machine Learning by Afshine Amidi and Shervine Amidi


## Motivation

Robotics.

## Topics

- History
 - General
	 - Definition of Machine Learning
	 - Linear vs Non-linear Algorithms
	 - Supervised vs Unsupervised vs Semi-Supervised Learning
	 - Bias-Variance trade-off
	 - Underfitting and Overfitting
- Optimization
	- Gradient Descent
- Supervised Learning
- Unsupervised Learning

## History

- Samuel's Checker Player (1952)
- Perceptron (1957)
- AI Winter: Minsky & Papert "killed" AI (1969)
- TD-Gammon (1994)
- Deep Blue (1997)
- Tom Michel (1999) "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

## General

**Definition**

*What is Machine Learning?* Algorithms that improve on some task with experience. Based on Statistics and Optimization, not logic.

We want to learn a target function $$f$$ that maps input variable $$X$$ to output variable $$Y$$, with an error $$e$$:

$$Y = f(X) + e$$

**Linear vs Non-linear Models**

Linear models are usually simpler, faster, and require less data whereas non-linear algorithm are more flexible, more powerful (they can represent a larger class of functions), and more performant but much harder to train.

 - **Linear (or parametric)**: models that first make an assumption about a function form, or shape, of $$f$$ (linear). Then fits the model. This reduces estimating $$f$$ to just estimating set of parameters, but if our assumption was wrong, will lead to bad results.
 - **Non-linear (or non-parametric)**: models that don’t make any assumptions about $$f$$, which allows them to fit a wider range of shapes; but may lead to overfitting

**Supervised vs Unsupervised vs Semi-Supervised Learning**

- **Supervised learning** methods learn to predict Y from X given that the data is labeled.
- **Unsupervised learning** where all data is unlabeled and the algorithms learn to inherent structure from the input data.
- **Semi-Supervised Learning** methods have some data labeled but most of it is unlabeled.

![enter image description here](https://4.bp.blogspot.com/-mC4Sn0NKt0k/XyBRb-5PUYI/AAAAAAAAJpY/c2p7dv0k3CUprTpu73oDYl6G12QsZAIHACLcBGAsYHQ/s1600/supervised.jpg)

**Feature engineering**

The process of using domain knowledge to create features or input variables that help machine learning algorithms perform better. Done correctly, it can help increase the predictive power of your models. Feature engineering is more of an art than science. FE is one of the most important steps in creating a good model. 

As Andrew Ng puts it: "Coming up with features is difficult, time-consuming, requires expert knowledge. ‘Applied machine learning’ is basically feature engineering."

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
- Calculate cost: $$J(\theta)=evaluate(f(coefficients))$$
- Gradient of the cost: $$\frac{\delta}{\delta\theta_J}J(\theta)$$
- Update coefficients: $$\theta_j =\theta_j - \alpha \frac{\delta}{\delta\theta_J}J(\theta)$$

The cost updating process is repeated until convergence or until minimum is found.

**Ordinary Least Squares**

**Maximum Likelihood Estimation**


# Supervised Learning

Given a set of data points $$[ x (1), ..., x(m) ]$$ associated to a set of outcomes $$[y (1), ..., y(m)]$$, we would like to learn a function $$h$$ such that for a new pair belonging to some distribution $$(x,y)∼P$$, we have $$h(x)=y$$ with high probability (or $$h(x)≈y$$).

## Types of Prediction

|  |  |
|--|--|
| Binary classification | *Eg.* spam filtering. An email is either spam (+1), or not (−1). |
| Multi-class classification | *Eg.* face classification. A person can be exactly one of K identities (e.g., 1="Barack Obama", 2="George W. Bush", etc.). |
| Regression | *Eg.* predict future temperature or the height of a person. |

## Hypothesis

Before we can find a function $$h$$, we must specify what type of function it is that we are looking for. It could be an artificial neural network, a decision tree or many other types of classifiers. 

**No Free Lunch Theorem** No single machine learning algorithm is better than all the others on all problems. It is common to try multiple models and find one that works best for a particular problem.

## Loss Function

A loss function evaluates a hypothesis $$h ∈ H$$ on our training data and tells us how bad it is. The higher the loss, the worse it is - a loss of zero means it makes perfect predictions.

-   Regression Loss Functions
    -   Mean Squared Error Loss (**L2 Loss**)
    -   Mean Absolute Error Loss (**L1 Loss**)
    -   Huber Loss
-   Binary Classification Loss Functions
    -   Binary Cross-Entropy (**Log Loss**)
    -   Hinge Loss
-   Multi-class Classification Loss Functions
    -   Multi-class Cross Entropy Loss
    -   Kullback Leibler Divergence Loss

## Cost Function

The cost function $$J$$ is commonly used to assess the performance of a model, and is defined with the loss function L as follows:




# Modeling - Evaluation Metrics

To determine how good our model is, best way to assess is to use data points your model has never seen. 

## Regression Task



## Classification Task

