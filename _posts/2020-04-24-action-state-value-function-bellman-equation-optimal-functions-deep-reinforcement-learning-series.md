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
- The optimal state value function, $$v_*(s) = max_{\pi} v_{\pi}(s)$$, is the maximum value function over all policies.
- The optimal action-value function, $$q_*(s, a) = max_{\pi} a_{\pi}(s, a)$$, is the maximum action-value function over all policies

## Topics
- [1. Rewards](#1-rewards)
- [2. Policy](#2-policy)
- [3. Bellman Equations](#3-bellman-equations)

## 1. Rewards

In RL, agents goal is to maximize the cumulative future reward or cumulative reward, $$R_t$$ it receives over time. The agents take action and receives reward at each time step. Each of the subsequences of time steps are called episodes or plays of a game. Mathematically, we can write the cumulative future reward as:

$$R_t = r_{t+1} + r_{t+2} + r_{t+3} + r_{t+4} + ... = \Sigma_{k=0}^{\infty}{r_{t+k+1}}$$

However, future rewards are uncertain so we should use future cumulative discounted reward.

$$R_t = \gamma^{0} r_{t+1} + \gamma^{1} r_{t+2} + \gamma^{2} r_{t+3} + \gamma^{3} r_{t+4} + ... = \Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+1}}$$

where $$\gamma$$ is between $$[0, 1]$$. The advantage to using discounted rewards is that we can give greater weight to sooner rewards, meaning we care more about immediate rewards and less about rewards we will receive further in the future. If gamma is 1, we care about all rewards equally. If gamma is 0, we only care about the immediate reward and do not care about any reward after that.

## 2. Policy

A policy describes how the agents should act. Agents take actions based on the policy written $$\pi(s, a)$$. The input to a policy function is the current state and the action the user wants to take, and it returns the probability of taking that action in that state. 

Our goal is to learn an optimal policy which tells us how to act to maximize return in every state. The optimal policy can be deterministic (1 decision in each state) or stochastic (multiple possible decisions in each state).

To learn the optimal policy, we have to make use of the  **state value function V(state)**, and the  **action value function Q(state, action)**.

The  **state value function** $$V^{\pi}(s)$$  describes the value of a state when following a policy. It is the expected return when starting in state s and acting according to our policy. The state value function equation is given by:

$$V^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [R_t \vert s_t = s]$$

The  **action value function**  _Q(state, action)_ describes the value of taking an action in some state when following a policy. It is the expected return given the state and action under a policy:

$$Q^{\pi}(s, a) = \mathop{\mathbb{E}}_{\pi} [R_t \vert s_t = s, a_t = a]$$

## 3. Bellman Equations

