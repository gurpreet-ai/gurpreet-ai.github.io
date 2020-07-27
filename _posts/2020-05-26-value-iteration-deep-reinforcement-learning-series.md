---
layout: post
title:  "Value Iteration - Dynamic Programming Approach - Deep Reinforcement Learning Series"
date:   2020-05-06 12:00:00
---

## Article Goal

In this article, our goal will be to implement **Value Iteration algorithm** to compute the value functions, $$v^*$$ or $$q^*$$. We can easily obtain optimal policies once we have found the optimal value functions. Value Iteration algorithm use a dynamic programming (DP) approach where we have complete knowledge of the environment or all the MDP variables. 

Unlike policy iteration, where the policy is continually evaluated and improved, in value iteration the policy is derived when value iteration is complete.

## 1. Value Iteration

In value iteration, we start off with a random value function from which we can drive some non-optimal policy. We look for a new improved value function in iterative fashion until we find the optimal value function. Once we find the optimal value function, we can derive an optimal policy from it.

## 2. Algorithm

![value_iteration_algorithm](https://1.bp.blogspot.com/-5E2RlIH-2Po/Xx9JtKwDFRI/AAAAAAAAJo4/165pJrrMPIYzVRZ1Z6QWaHSV3Kf9eTdNwCLcBGAsYHQ/s1600/policy_iteration_3.png)

## 3. Implementation


```python
import numpy as np

def value_iteration(env, gamma, theta):
    """
    value_iteration: 
    
    @param env:            OpenAI Gym environment
    @param gamma:          discount factor
    @param theta:          the evaluation will stop once values for all states are less than the threshold
    
    @return state_values:   inital state values
    @return policy:         policy matrix containing actions and their probability in each state
    """
    state_len = env.nS
    action_len = env.nA
    
    delta = theta*2
    
    # initialize state value estimates
    states_values = np.zeros((state_len))
    
    # loop until convergence in state values
    while delta > theta:
        delta = 0
        # for all states
        for s in range(state_len):
            # new state values array for all actions
            temp_array = np.zeros((action_len))
            # for all actions
            for a in range(action_len):
                transition_list = env.P[s][a]
                # for all probability transitions from current state
                for i in transition_list:
                    transition_prob, next_state, reward, done = i
                    if (done):                    
                        temp_array[a] += transition_prob * reward
                    else:
                        temp_array[a] += transition_prob * (reward + gamma * states_values[next_state])
            # max state value
            v_max = np.max(temp_array)
            # compare old delta with new delta
            delta = max(delta, np.abs(v_max - states_values[s]))
            states_values[s] = v_max
            
    # extract the policy from states
    policy = np.zeros((state_len, action_len))
    for s in range(state_len):
        temp_array = np.zeros((action_len))
        for a in range(action_len):
            transition_list = env.P[s][a]
            for i in transition_list:
                transition_prob, next_state, reward, done = i
                temp_array[a] += transition_prob * (reward + gamma * states_values[next_state])
        # take max action every time
        policy[s, np.argmax(temp_array)] = 1
    
    return states_values, policy
```


```python
import gym

# use the frozen lake env
env = gym.make('FrozenLake-v0', is_slippery=False)

# discount factor gamma
gamma = 0.99

# threshold
theta = 0.0001

n_state = env.observation_space.n
print("N states (4x4):", n_state)
n_action = env.action_space.n
print("M actions (U, D, L, R):", n_action)

env.reset()
print("\nFrozenLake-v0 Env (H: hole, S: start, G: Goal, F: Frozen)")
env.render()
```

    N states (4x4): 16
    M actions (U, D, L, R): 4
    
    FrozenLake-v0 Env (H: hole, S: start, G: Goal, F: Frozen)
    
    [41mS[0mFFF
    FHFH
    FFFH
    HFFG



```python
# call the policy iteration method
states_values, policy = value_iteration(env, gamma, theta)
```


```python
# state values are higher close to the goal
print(np.round(states.reshape(4,4),3))
```

    [[0.951 0.961 0.97  0.961]
     [0.961 0.    0.98  0.   ]
     [0.97  0.98  0.99  0.   ]
     [0.    0.99  1.    0.   ]]



```python
# policy shows the optimal action to take in the grid world
print(np.round(policy.reshape(16,4),3))
```

    [[0. 1. 0. 0.]
     [0. 0. 1. 0.]
     [0. 1. 0. 0.]
     [1. 0. 0. 0.]
     [0. 1. 0. 0.]
     [1. 0. 0. 0.]
     [0. 1. 0. 0.]
     [1. 0. 0. 0.]
     [0. 0. 1. 0.]
     [0. 1. 0. 0.]
     [0. 1. 0. 0.]
     [1. 0. 0. 0.]
     [1. 0. 0. 0.]
     [0. 0. 1. 0.]
     [0. 0. 1. 0.]
     [1. 0. 0. 0.]]

