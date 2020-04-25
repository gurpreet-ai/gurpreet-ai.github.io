---
layout: post
title:  "Common Approaches in Reinforcement Learning - Deep Reinforcement Learning Series"
date:   2020-04-26 12:00:00
---

## Article Goal

Before we dive into deep reinforcement learning, we should learn about the different approaches in reinforcement learning. In this article, we'll briefly talk about Dynamic Programming (DP), Monte Carlo (MC) Methods, Temporal-Difference (TD) Learning, and Policy Gradients (PG) methods. These approaches in reinforcement learning are important to understand before diving into deep reinforcement learning approaches.


# Topics
- [1. Dynamic Programming (DP)](#1-dynamic-programming)
- [2. Monte Carlo (MC) Methods](#2-monte-carlo-methods)
- [3. Temporal-Difference (TD) Learning](#3-temporal-difference-Learning)
- [4. Policy Gradient Methods](#4-policy-gradient)

## 1. Dynamic Programming (DP)

If we have complete knowledge of the environment or all the MDP variables (5-tuple $$(S, A, P(s_{t+1} \vert s, a), R(s, a, s_{t+1}), \gamma)$$), following Bellman equations, we can use DP to iteratively evaluate value functions and improve policy. DP methods are known as model-based methods because we have complete knowledge of the environment. We will talk about policy iteration and the value iteration DP algorithm in the next article.

## 2. Monte Carlo (MC) Methods

However, in most cases, we do not know the $$P(s_{t+1}, r \vert s, a), R(s, a, s_{t+1})$$, so we cannot solve MPDs by directly using the bellman equations. This is where Monte Carlo (MC) methods becomes helpful. MC methods are model-free and learns directly from episodes of experience without any prior knowledge of MDP transition function P(s′,r|s,a) and rewards function R(s,a). However, this can only be applied to episodic MDPs because an episode has to terminate before we can calculate any returns. Here, we do not do an update estimates after every action, but rather after every episode. 

## 3. Temporal-Difference (TD) Learning

TD learning is a combination of DP and MC methods. Like MC methods, TD methods are model-free meaning these methods can learns from episodes with no prior knowledge of the environment. Like DP, TD methods update estimates iteratively based in part on other learned estimates, without waiting for the final outcome.

## 4. Policy Gradient Methods

DP, MC, TD are all action-value methods. They learn the values of actions and then selected actions based on their estimated action values. Their policies would not even exist without the action-value estimates. Policy Gradient methods learn a parameterized policy that can select actions without consulting a value function. A value function may still be used to learn the policy parameter, but is not required for action selection.


We will be going over methods from each of the approches in the next articles.