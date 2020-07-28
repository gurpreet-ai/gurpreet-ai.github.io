---
layout: post
title:  "Machine Learning Cheatsheet"
date:   2020-07-28 12:00:00
---



## Goal

The goal of this cheatsheet is to briefly summarize machine learning algorithms, advantages, and use cases. I want to reference the original Machine Learning Cheatsheet written by Remi Canard. Thank you Remi.

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

**Bias-Variance trade-off**

In supervised learning, the prediction error $$e$$ is composed of the bias, the variance, and the irreducible part.

 - **Bias** refers to simplifying assumptions made to learn the target function easily.
 - **Variance** refers to sensitivity of the model to changes in the training data.

The goal of parametrization (writing in terms of parameters) is to achieve a low bias (underlying pattern not too simplified), and low variance (not sensitive to the specificities of the training data) tradeoff.

**Underfitting and Overfitting**

In statistics, fit refers to how well the target function is approximated. 

 - **Underfitting** refers to poor inductive learning from training data and poor generalization.
 - **Overfitting** refers to learning the training data detail and noise which leads to poor generalization. It can be limited by using resampling, and defining a validation dataset.


## Optimization

