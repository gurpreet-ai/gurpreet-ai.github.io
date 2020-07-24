---
layout: post
title:  "Value Iteration - Dynamic Programming Approach - Deep Reinforcement Learning Series"
date:   2020-05-06 12:00:00
---

## Article Goal

In this article, our goal will be to implement one of the powerful algorithm called **Value Iteration algorithm** to compute the value functions, $$v^*$$ or $$q^*$$. We can easily obtain optimal policies once we have found the optimal value functions. Value Iteration algorithm use a dynamic programming (DP) approach where we have complete knowledge of the environment or all the MDP variables. 

In DP, instead of solving complex problems one at a time, we break the problem into simple sub-problems, then for each sub-problem, we compute and store the solution. If the same sub-problem occurs, we will not recompute, instead, we use the already computed solution.

## 1. Bellman Equations


## 2. Value Iteration

In value iteration, we start off with a random value function from which we can drive some non-optimal policy. We look for a new improved value function in iterative fashion until we find the optimal value function. Once we find the optimal value function, we can derive an optimal policy from it.


## 2. 