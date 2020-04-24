---
layout: post
title:  "Action/State Value Functions, Bellman Equations, Optimal Action/State Value Functions - Deep Reinforcement Learning Series"
date:   2020-04-24 12:00:00
---

## Article Goal

The bellman equation was derived by an American Mathematician by the name Richard Bellman to solve Markov Decision Processes (MDPs). In this article, my goal is to derive the Bellman equation for the state value function, $$V(s)$$ and the action value function, $$Q(s, a)$$. Most reinforcement learning algorithms are based on estimating state value or action value functions. 
- The state value function tells us the value for being in some state when following some policy. 
- The action value function tells us the value of taking an action in some state when following a certain policy.

After we derive the state value function, $$V(s)$$ and the action value function, $$Q(s, a)$$, we will explain how to find the optimal state value function and the optimal action value function.

## Topics
- [1. Rewards](#1-rewards)

## 1. Rewards

In RL, agents goal is to maximize the cumulative future reward 