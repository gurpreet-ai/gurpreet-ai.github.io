---
layout: post
title:  "Action/State Value Functions, Bellman Equations, Optimal Action/State Value Functions - Deep Reinforcement Learning Series"
date:   2020-04-24 12:00:00
---

## Article Goal

The bellman equation was derived by American mathematician Richard Bellman to solve Markov Decision Processes (MDPs). In this article, my goal is to derive the Bellman equation for the state value function, $$V(s)$$ and the action value function, $$Q(s, a)$$. **Most reinforcement learning algorithms are based on estimating value function** (state value function or state-action value function). The value functions are functions of states (or of state–action pairs) that estimate how good it is for the agent to be in a given state (or how good it is to perform a given action in a given state).
- The state value function tells us the value for being in some state when following some policy. 
- The action value function tells us the value of taking an action in some state when following a certain policy.

After we derive the state value function, $$V(s)$$ and the action value function, $$Q(s, a)$$, we will explain how to find the optimal state value function and the optimal action value function.
- The optimal state value function, $$v_*(s) = max_{\pi} v_{\pi}(s)$$, is the maximum value function over all policies.
- The optimal action-value function, $$q_*(s, a) = max_{\pi} a_{\pi}(s, a)$$, is the maximum action-value function over all policies

## Topics
1. [Rewards](#1-rewards)
2. [Policy](#2-policy)
3. [Transition Probability Distribution and Expected Reward](#3-transition-probability-distribution-and-expected-reward)
4. [Bellman Equation for State Value function, $$V(s)$$](#4-bellman-equation-state-value-function)
5. [Bellman Equation for State-Action Value function, $$V(s)$$](#5-bellman-equation-state-action-value-function)
6. [Optimal Bellman Equation](#6-optimal-bellman-equation)

## 1. Rewards

In RL, agents goal is to maximize the cumulative future reward or cumulative reward, $$G_t$$ it receives over time. The agents take action and receives reward at each time step. Each of the subsequences of time steps are called episodes or plays of a game. Mathematically, we can write the cumulative future reward as:

$$G_t = R_{t+1} + R_{t+2} + R_{t+3} + R_{t+4} + ... = \Sigma_{k=0}^{\infty}{r_{R+k+1}}$$

However, future rewards are uncertain so we should use future cumulative discounted reward.

$$G_t = \gamma^{0} r_{t+1} + \gamma^{1} r_{t+2} + \gamma^{2} r_{t+3} + \gamma^{3} r_{t+4} + ... = \Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+1}}$$

where $$\gamma$$ is between $$[0, 1]$$. The advantage to using discounted rewards is that we can give greater weight to sooner rewards, meaning we care more about immediate rewards and less about rewards we will receive further in the future. If gamma is 1, we care about all rewards equally. If gamma is 0, we only care about the immediate reward and do not care about any reward after that.

## 2. Policy

A policy describes how the agents should act. Agents take actions based on the policy written $$\pi(s, a)$$. The input to a policy function is the current state and the action the user wants to take, and it returns the probability of taking that action in that state. 

Our goal is to learn an optimal policy which tells us how to act to maximize return in every state. The optimal policy can be deterministic (1 decision in each state) or stochastic (multiple possible decisions in each state).

To learn the optimal policy, we have to make use of the  **state value function V(state)**, and the  **action value function Q(state, action)**.

The  **state value function** $$V^{\pi}(s)$$  describes the value of a state when following a policy. It is the expected return when starting in state $$s$$ and acting according to our policy. The state value function equation is given by:

$$V^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [G_t \vert s_t = s]$$

The  **action value function**  $$Q(s, a)$$ describes the value of taking an action in some state when following a policy. It is the expected return given the state and action under a policy:

$$Q^{\pi}(s, a) = \mathop{\mathbb{E}}_{\pi} [G_t \vert s_t = s, a_t = a]$$

## 3. Transition Probability Distribution and Expected Reward

To derive the bellman equations, we need to define some useful notation. In finite MDP, the set of states, actions, and rewards all have a finite number of elements, therefore we have a well defined discrete transition probability distributions dependent only on the preceding state and action. The **transition probability distribution**  if we start in state $$s$$, and take action $$a$$, we end up in new state $$s' \in S$$ with a reward $$r \in R$$ is given by:

$$ p(s', r, \vert s, a) = Pr(S_t = s', R_t = r | S_{t-1} = s, A_{t-1} = a)$$

Probability distribution for each choice of $$s$$ and $$a$$ sum to 1.

$$ \Sigma_{s' \in S} \: \Sigma_{r \in R} \ p(s', r, \vert s, a) = 1$$

The expected reward that we receive when starting in state $$s$$, taking action $$a$$, and moving into state $$s'$$ (state–action–next-state triples) is written as:

$$  r(s, a, s') = \mathbb{E}[R_{t} \vert S_{t-1} = s, A_{t-1} = a, S_{t} = s']$$

## 4. Bellman Equation for the State Value Function, $$V(s)$$

Now, we will derive the bellman equation for the state value function, **V(state)**. Remember that the value function of a state $$s$$ under a policy $$\pi$$, denoted $$v_{\pi}$$, is the expected return when starting in $$s$$, and following $$\pi$$ thereafter. We can rewrite the state value function equation from earlier as:

$$V^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [G_t \vert S_t = s]$$

$$V^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [G_t = \gamma^{0} r_{t+1} + \gamma^{1} r_{t+2} + \gamma^{2} r_{t+3} + \gamma^{3} r_{t+4} + ... \vert S_t = s]$$

$$V^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [\Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+1}} \vert S_t = s ]$$

We can pull out the first reward from the sum inside the expectation:

$$V^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [R_{t+1} + \gamma \Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+2}} \vert S_t = s ]$$

Replace the summation inside:

$$V^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [R_{t+1} + \gamma G_{t+1} \vert S_t = s ]$$

This expectation means what we expect the reward to be if we continue from state $$s$$ following some policy. We can split this expectation into two expectations since it's addition. We can combine them after we compute each expecatation.

$$\mathop{\mathbb{E}}_{\pi} [R_{t+1} \vert S_t = s ]$$

$$\mathop{\mathbb{E}}_{\pi} [\gamma G_{t+1} \vert S_t = s ]$$

The first expectation:

$$\mathop{\mathbb{E}}_{\pi} [R_{t+1} \vert S_t = s ]  = \Sigma_a \ \pi(s, a) \ \Sigma_{s'} \ p(s', r, \vert s, a) \ r(s, a, s') \ $$

That is the expectation of reward at time $$t + 1$$ given state $$s$$, which is the reward over all actions the agent can take and end up in all the possible new states which have a transition probability and a reward associated with it. Simply, we are summing over all possible actions and all possible returned states that we may end up in, and the reward for going into those states.

The second expectation:

$$\mathop{\mathbb{E}}_{\pi} [\gamma \ G_{t+1} \vert S_t = s ] = \mathop{\mathbb{E}}_{\pi} [\gamma \ \Sigma_{k=0}^{\infty}{ \ \gamma^{k} \ r_{t+k+2}} \vert S_t = s ]$$

We can take the gamma out:

$$\mathop{\mathbb{E}}_{\pi} [\gamma \ G_{t+1} \vert S_t = s ] = \gamma \ \mathop{\mathbb{E}}_{\pi} [\Sigma_{k=0}^{\infty}{ \ \gamma^{k} \ r_{t+k+2}} \vert S_t = s ]$$

$$\mathop{\mathbb{E}}_{\pi} [\Sigma_{k=0}^{\infty}{ \ \gamma^{k} \ r_{t+k+2}} \vert S_t = s ] = \Sigma_a \ \pi(s, a) \ \Sigma_{s'} \ p(s', r, \vert s, a) \  \mathop{\mathbb{E}}_{\pi} [\Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+2}} \vert S_{t+1} = s' ]$$

We know from earlier that:

$$V^{\pi}(s') =  \mathop{\mathbb{E}}_{\pi} [\Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+2}} \vert S_{t+1} = s' ]$$

$$\mathop{\mathbb{E}}_{\pi} [\Sigma_{k=0}^{\infty}{ \ \gamma^{k} \ r_{t+k+2}} \vert S_t = s ] = \Sigma_a \ \pi(s, a) \ \Sigma_{s'} \ p(s', r, \vert s, a) \ V^{\pi}(s')  $$

Finally, the second expectation looks like:

$$\mathop{\mathbb{E}}_{\pi} [\gamma \ G_{t+1} \vert S_t = s ] = \Sigma_a \ \pi(s, a) \ \Sigma_{s'} \ p(s', r, \vert s, a) \ \gamma \ V^{\pi}(s')$$

We can combine the two expectations and get the final form of the Bellman Equation for value state function:

$$V^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [R_{t+1} + \gamma G_{t+1} \vert S_t = s ]$$

$$V^{\pi}(s) = \Sigma_a \ \pi(s, a) \ \Sigma_{s'} \ p(s', r, \vert s, a) \ [r(s, a, s') \ + \ \gamma \ V^{\pi}(s')] $$


## 5. Bellman Equation for State-Action Value function

We can compute the state-action value function similarly.

$$Q^{\pi}(s, a) = \mathop{\mathbb{E}}_{\pi} [G_t \vert S_t = s, A_t = a]$$

$$Q^{\pi}(s) = \mathop{\mathbb{E}}_{\pi} [G_t = \gamma^{0} r_{t+1} + \gamma^{1} r_{t+2} + \gamma^{2} r_{t+3} + \gamma^{3} r_{t+4} + ... \vert S_t = s, A_t = a]$$

$$Q^{\pi}(s, a) = \mathop{\mathbb{E}}_{\pi} [\Sigma_{k=0}^{\infty}{ \ \gamma^{k}r_{t+k+1}} \vert S_t = s, A_t = a]$$

Take the first reward out of the summation:

$$Q^{\pi}(s, a) = \mathop{\mathbb{E}}_{\pi} [R_{t+1} + \gamma \ \Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+2}} \vert S_t = s, A_t = a]$$

We can separate the two expectations:

$$\mathop{\mathbb{E}}_{\pi} [R_{t+1} \ \vert \ S_t = s, A_t = a]$$

$$\mathop{\mathbb{E}}_{\pi} [\gamma \ \Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+2}} \ \vert \ S_t = s, A_t = a]$$

The first expectation:

$$\mathop{\mathbb{E}}_{\pi} [r_{t+1} \ \vert \ S_t = s, A_t = a]  = \Sigma_{s'} \ p(s', r, \ \vert \ s, a) \ r(s, a, s')$$

The second expectation:

$$\mathop{\mathbb{E}}_{\pi} [\gamma \ \Sigma_{k=0}^{\infty}{\gamma^{k}r_{t+k+2}} \ \vert \ S_t = s, A_t = a]$$

can also be written as:

$$\mathop{\mathbb{E}}_{\pi} [\gamma \ G_t \ \vert \ S_t = s, A_t = a]$$

We take the gamma out of the expectation to make things simple for now:

$$\gamma \ \mathop{\mathbb{E}}_{\pi} [G_t \ \vert \ S_t = s, A_t = a]$$

$$\mathop{\mathbb{E}}_{\pi} [G_t \ \vert \ S_t = s, A_t = a]\ =  \Sigma_{s'} \ p(s', r, \ \vert \ s, a) \ \ \Sigma_{a'} \ \pi(s', a') \ \mathop{\mathbb{E}}_{\pi} [G_{t+1} \ \vert \ S_{t+1} = s', A_t = a'] $$

The second expectation is given by:

$$\mathop{\mathbb{E}}_{\pi} [\gamma \ G_t \ \vert \ S_t = s, A_t = a]\ =  \Sigma_{s'} \ p(s', r, \ \vert \ s, a) \ \gamma \ \Sigma_{a'} \ \pi(s', a') \ \mathop{\mathbb{E}}_{\pi} [G_{t+1} \ \vert \ S_{t+1} = s', A_t = a'] $$

Combining both expectations:

$$Q^{\pi}(s, a) = \Sigma_{s'} \ p(s', r, \ \vert \ s, a) \ [r(s, a, s') \ + \ \gamma \ \Sigma_{a'} \ \pi(s', a') \ \mathop{\mathbb{E}}_{\pi} [G_{t+1} \ \vert \ S_{t+1} = s', A_t = a'] ] $$

$$Q^{\pi}(s, a) = \Sigma_{s'} \ p(s', r, \ \vert \ s, a) \ [r(s, a, s') \ + \ \gamma \ \Sigma_{a'} \ \pi(s', a') \ Q(s', a')] $$

## 6. Optimal Bellman Equation

We know now how to make a decision on what action to take if an agent is in a particular state using a policy. Some policies may perform better than other policies and vice versa. Remember in reinforcement learning, our goal is to maximize reward over a period of time that it takes for an agent to complete some task using some policy.

So we need to find an optimal policy and that will give us the highest reward. Optimal policies can be denoted by $$\pi^*$$.

The optimal state value function is written as $$v^{*}(s)$$. It is given by:

$$v^*(s) = max_{\pi} \ v_{\pi} (s)$$

This is the **Bellman Optimality Equation** $$v_*(s)$$ for State Value function.

Intuitively, the Bellman optimality equation should output a value for a state under an optimal policy that must equal the expected return for the best action from that state.

$$v^*(s) = max_{a \in A} \ q_{\pi_*}(s, a)$$

$$v^*(s) = max_{a \in A}  \mathop{\mathbb{E}}_{\pi_*} [G_t \ \vert \ S_t = s, A_t = a]$$

$$v^*(s) = max_{a \in A}  \mathop{\mathbb{E}}_{\pi_*} [R_{t+1} + \gamma G_{t+1}\ \vert \ S_t = s, A_t = a]$$

$$v^*(s) = max_{a \in A}  \mathop{\mathbb{E}}_{\pi_*} [R_{t+1} + \gamma v_*(S_{t+1}) \ \vert \ S_t = s, A_t = a]$$

$$v^*(s) = max_{a \in A}  \Sigma p(s', r \ \vert \ s, a)[r + \gamma v_*(s')]$$

The Bellman optimality equation for $$q_*(s)$$ State-Action Value function is:

$$q_*(s, a) = \mathop{\mathbb{E}} [R_{t+1} + \gamma \ max_{a \in A} \ q_* (S_{t+1}, a') \ \vert \ S_t = s, A_t = a]$$

$$q_*(s, a) = \Sigma_{s', r} \ p(s', r \ \vert \ s, a) [r + \gamma \ max_{a'}  \ q_*(s', a')$$
