---
layout: post
title:  "Iterative Policy Evaluation - Dynamic Programming Approach - Deep Reinforcement Learning Series"
date:   2020-05-01 12:00:00
---

## Article Goal

In this article, our goal will be to implement our first reinforcement learning algorithm called **Iterative Policy Evaluation**. This algorithm uses the dynamic programming approach. 

As the name implies, this is a **iterative algorithm** used to evaluate a given policy, **estimate state value** for all the states in the environment, and it will **output the best state-value function**, $$V^{\pi}$$, for the policy. The best value function will give most reward.

## 1. Iterative Policy Evaluation Algorithm

To calculate the state values for a given policy, we will directly apply the bellman equation. Bellman equation gives us a recursive expression for the value function $$V_{\pi}$$.

$$V^{\pi}(s) = \Sigma_a \ \pi(s, a) \ \Sigma_{s'} \ p(s', r, \vert s, a) \ [r(s, a, s') \ + \ \gamma \ V^{\pi}(s')] $$

This equation can be modified to create an update rule for our algorithm. 

$$V_{k+1}(s) = \Sigma_a \ \pi(s, a) \ \Sigma_{s'} \ p(s', r, \vert s, a) \ [r(s, a, s') \ + \ \gamma \ V_{k}(s')] $$

The key idea is that we start with some initial policy and we use the update rule or the bellman equation to update the state value function to produce a better approximation of the value function. Next we calculate the difference between the previous and current values for all state value and if the difference is smaller than some $$\theta$$, we can assume that current state value function is optimal for the given policy. The algorithm is shown in the image below.

![enter image description here](https://2.bp.blogspot.com/-F8JOCry9Eyk/XxsbxVjwMeI/AAAAAAAAJn8/zIhhPXDA4DQTpMDktpXaTWaSndA29UA3gCLcBGAsYHQ/s1600/iterative_policy_evaluation_algorithm.png)

## 2. Iterative Policy Evaluation Implementation

We will implement the Iterative Policy Evaluation Implementation algorithm in python. We will use the Frozen Lake game as our environment.

![enter image description here](https://2.bp.blogspot.com/-R2ilUQbMTNg/XxscKr7n8WI/AAAAAAAAJoE/LtmjzcThousFBQzlqY7yDUzUxcI-Z96dACLcBGAsYHQ/s100/frozen_lake.png)

The goal of Frozen Lake game is to go from the starting state (S) to the goal state (G) by walking only on frozen tiles (F) and avoid holes (H).

[Read more about FrozenLake v0](https://github.com/openai/gym/wiki/FrozenLake-v0)

```python
import gym

env = gym.make("FrozenLake-v0")

n_state = env.observation_space.n
print("N states (4x4):", n_state)
n_action = env.action_space.n
print("M actions (U, D, L, R):", n_action)

env.reset()
print("\nFrozenLake-v0 Env")
env.render()
```

    N states (4x4): 16
    M actions (U, D, L, R): 4
    
    FrozenLake-v0 Env
    
    [41mS[0mFFF
    FHFH
    FFFH
    HFFG



```python
# env model: we have knowledge about everything in the environment

import pprint
pp = pprint.PrettyPrinter(indent=4)
pp.pprint(env.P)

# {
#     state1: {
#         action1: [(transition_prob, next_state, reward, done)],
#         action2: [(transition_prob, next_state, reward, done)],
#         action3: [(transition_prob, next_state, reward, done)],
#         action4: [(transition_prob, next_state, reward, done)],
#     },
#     state2: {
#         action1: [(transition_prob, next_state, reward, done)],
#         ...
#     }
#     ...
# }

```

```python
import numpy as np

def policy_evaluation(env, policy, gamma, theta, state_values):
    """
    policy_evaluation: 		estimate state values based on the policy
    
    @param env:       		OpenAI Gym environment
    @param policy:    		policy matrix containing actions and their probability in each state
    @param gamma:     		discount factor
    @param threshold: 		the evaluation will stop once values for all states are less than the threshold
    @param state_values: 	initial state values

    @return:         		new state values of the given policy
    """
    delta = theta*2
    state_len = env.nS
    action_len = env.nA
    while (delta > theta):
        delta = 0
        # for all state
        for s in range(state_len):
            # we will get new state value
            new_s = 0
            # for all actions
            for a in range(action_len):
                # get the current transitions list (U,D,L,R)
                transitions_list = env.P[s][a]
                # for all transitions from currect state
                for i in transitions_list:
                    transition_prob, next_state, reward, done = i
                    new_s += policy[s,a]*transition_prob*(reward+gamma*state_values[next_state])
        
            delta = max(delta, np.abs(new_s - state_values[s])) 
            state_values[s] = new_s
    return state_values

# discount factor gamma
gamma = 0.99
# intial policy: agents can take actions at equal probability
policy = np.ones((n_state, n_action))/n_action
# initial state values
state_values = np.zeros(n_state)
theta = 0.0001


print("****** Intial policy ******")
print(policy)
print("****** Gamma (discount factor) ******")
print(gamma)
print("****** Theta ******")
print(theta)
state_values = policy_evaluation(env, policy, gamma, theta, state_values)
print("****** Best state values ******")
print(np.round(state_values.reshape(4,4), 3))
print("NOTICE: state values are higher as you get closer to the goal.")
```

    ****** Intial policy ******
    [[0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]
     [0.25 0.25 0.25 0.25]]

    ****** Gamma (discount factor) ******
    0.99

    ****** Theta ******
    0.0001

    ****** Best state values ******
    [[0.012 0.01  0.019 0.009]
     [0.015 0.    0.039 0.   ]
     [0.033 0.084 0.138 0.   ]
     [0.    0.17  0.434 0.   ]]

    NOTICE: state values are higher as you get closer to the goal.

