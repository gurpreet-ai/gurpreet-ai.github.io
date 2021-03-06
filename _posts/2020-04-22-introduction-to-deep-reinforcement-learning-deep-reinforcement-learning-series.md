---
layout: post
title:  "Introduction to Deep Reinforcement Learning - Deep Reinforcement Learning Series"
date:   2020-04-22 12:00:00
---

Reinforcement learning is currently one of the most active areas of research in artificial intelligence because of its combination with deep learning makes it possible to solve complex and challenging problems with high dimentional state-space. In this series of articles, I will dive into the area of deep reinforcement learning. But before I talk about it, I need to make sure you understand basic concepts in reinforcement learning and deep learning.

# Series Goal
The goal of this series is to give the reader an introduction to deep reinforcement learning, skills on how to create deep RL models using pytorch and learn deep RL algorithms. You can be a beginner in artifical intelligence to follow this series but you should have an intuitive understanding of how neural networks work.

# Motivation to learn Deep Reinforcement Learning

AlphaGo used deep reinforcement learning techniques to beat Lee Sedol, a South Korean professional Go player, in the game of Go (more complex than chess because of the number of possible moves at each turn). Many applications in robotics swarm.

# Article Goal
The goal of this article is to explain what is reinforcement learning (RL), how to formulate a RL problem, types of RL methods, and finally what is deep learning and how it has been combined with RL to create deep reinforcement learning.

# Topics
- [1. What is reinforcement learning?](#1-what-is-reinforment-learning)
- [2. Formulate RL problems](#2-formulate-rl-problems)
- [3. Types of reinforcement learning methods](#2-types-of-reinforcement-learning-methods)
- [4. How it differs from supervised and unsupervised learning?](#4-how-it-differs-from-supervised-and-unsupervised-learning)
- [5. What is deep learning?](#5-what-is-deep-learning)

## 1. What is reinforcement learning?

Reinforcement learning (RL) is a type of machine learning where learning for agents occurs by interacting with an environment. The agents are not taught what actions to take instead they learn from the consequences of its actions.

![rl]

[rl]: https://1.bp.blogspot.com/-44GqZioqWjg/XYLuJisPCOI/AAAAAAAAHMc/Uenl4uwY7QEiBetF5xAgZiNeateWfuAXACLcBGAsYHQ/s1600/RL.png "Image from Sutton and Barto – Reinforcement Learning: An Introduction"

Figure 1. Image from Sutton and Barto – Reinforcement Learning: An Introduction

The image in Figure 1. from the famous book on RL by Sutton and Barto clearly explains the RL concept. It shows that agents interact with an environment in discrete time-steps and at each time-step, the agent observes the environment, then takes an action and receives a numeric reward based on the action. If the action gets the agent closer to the goal, the reward may be positive or bigger and if it gets the agent further from the goal the reward may be negative or smaller. 

The goal of the agent is to maximize the reward. Imagine you are trying to teach a dog to catch a ball. You cannot teach the dog to explicitly catch a ball; instead you throw a ball, and every time it catches the ball, you give the dog a cookie. The cookie is the reward. The dog will learn that I get a cookie every time I catch the ball.

## 2. Formulate RL problems

RL problems are mathematically formulated with Markov Decision Processes (MDPs). MDPs are defined by the following parameters: a set of all possible states, a set of all possible actions, a reward function, and transition probabilities, which is the probability that the agent will move from one state to another. The figure below shows an example of MDPs:

![mdp]

[mdp]: https://1.bp.blogspot.com/-nFTBC6lSY3g/Xfg7IvM19iI/AAAAAAAAIJ0/NJVR5ylZSysHe71LM-pesMfiT0KKshtFwCLcBGAsYHQ/s1600/MDP.png "Figure 2. MDP Example from slides by Dan Klein, Pieter Abbeel, Anca Dragan"

The agents decides which action to take based on a policy. A policy can be deterministic or stochastic. Deterministic policies are used in environment where for every state you have a clear defined action you will take. Stochastic policies are used in environment where for every state, for you to take an action, you draw a sample from possible actions that follow a distribution. A policy is denoted by the symbol pi. We will go into details about policies later in this series but for now just know it is some oracle that agents talks with to figure out which action to take based on the current observations.

## 3. Types of reinforcement learning methods

There are four approaches to RL that we will be explaining in this series.

- **Dynamic Programming (DP)**: If we have complete knowledge of the environment or all the parameters of the MDP, we can get the optimal policy by using iteration methods. We will review value iteration and policy iteration methods in future articles.
- **Monte Carlo (MC)**: We do not have complete knowledge of the environment and are usually missing the transition probabilities or reward function from the MDP parameters. MC methods learn directly from episodes of experience without any prior knowledge of reward function or transition probabilities. But we need to wait for the episodes to finish before we can use that episode to learn.
- **Temporal Difference (TD) Learning**: Combination of DP and MC. Like DP, TD methods update estimates iteratively based in part on other learned estimates, without waiting for the episodes to finish. Like MC methods, TD methods can learn from episodes with no prior knowledge of the environment.
- **Policy Gradients**: Directly improve the policy by updating the policy parameter at each time step in the direction of an estimate of the gradient of performance.

## 4. How it differs from supervised and unsupervised learning?

In **supervised learning**, agents learn from training datasets which has a labeled set of inputs and outputs. The goal is to generalize learning so that we can generate the correct output for unseen inputs.

Examples of supervised learning includes the following:

- **Image classification**: hot dog or not hot dog? (labels are categorical)
- **Regression**: predicting house prices based (labels are continuous)

In **unsupervised learning**, we have to draw inferences from training dataset which only has a set of inputs and no known output labels for the inputs. The goal is to learn the hidden structure in the dataset.

Examples of unsupervised learning includes the following:

- **Clustering**: K-means
- **Dimensionality reduction**: PCA
- **Generative Adversarial Networks (GANs)**

## 5. What is deep learning?

Deep learning is another popular field of artificial intelligence. It is a framework for representation learning and it allows us to train an agent to predict output given a set of inputs. For example, we can train a model using deep learning to recognize cats in a photograph. It does this by using multi-layered neural networks. You can think that deep learning is basically large neural networks or deep neural networks (DNN) with big data requiring the use of many GPUs for computations to do representation learning.

In this series most of our examples can be run on CPUs and maybe trained faster using GPUs. We will use Google Colab for our examples.

## 6. What is deep reinforcement learning?

Deep Reinforcement Learning is the combination of reinforcement learning techniques with deep learning. This field has become popular since the success of Deep Q-Networks (DQN) introduced by DeepMind. Researchers at DeepMind used neural networks and showed that deep learning with convolutional layers can enable reinforcement learning algorithms to successfully learn to play Atari 2600 games. The only input used for training the networks was the pixel images and the game score. The performance on Atari games was impressive, as the learned policies were often able to outperform human players. This was a big milestone for deep reinforcement learning community. I will discuss more success as we move along with this series in the other articles.

Deep RL has applications in robotics, self-driving cars, healthcare, finance and many more. However, there are many challenges in applying deep RL algorithms such state space exploration. Thus, there are many algorithms proposed in literature that we will go over in this series along with cool projects.

Thank you for reading this article. You can share it and start reading the next article in the series.