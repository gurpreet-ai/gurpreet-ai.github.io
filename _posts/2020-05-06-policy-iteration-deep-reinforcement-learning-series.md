---
layout: post
title:  "Policy Iteration - Dynamic Programming Approach - Deep Reinforcement Learning Series"
date:   2020-05-06 12:00:00
---


## Article Goal

In this last article, we implemented the iterative policy evaluation algorithm to evaluate a policy. In this article, our goal will be to implement an algorithm called **Policy Iteration algorithm** which will help us improve a policy. Policy Iteration algorithm use a dynamic programming (DP) approach where we have complete knowledge of the environment or all the MDP variables.

## 1. Policy Iteration

**Policy Iteration** consists of two steps: **Policy improvement** and **policy evaluation**. We have already seen policy evaluation in the last article. Policy improvement tries to find the best action from all actions in all states. We alternate between the policy improvement and policy evaluation until converge on optimality.

![policy_iteration_convergence](https://2.bp.blogspot.com/-K3d4B9EKyAM/Xx8sztxH_kI/AAAAAAAAJoc/YpabFYqXDLg5VS32SXn3mYPysI-CCl0GwCLcBGAsYHQ/s1600/policy_iteration_1.png)

## 2. Algorithm

![policy_iteration_algorithm](https://3.bp.blogspot.com/-MgVsC80Z8tw/Xx8uR7rM_TI/AAAAAAAAJoo/FUDT7k58a4IkdHYojUD_BU5elxx_eYucgCLcBGAsYHQ/s1600/policy_iteration_2.png)

## 3. Implementation

```python
import numpy as np

def policy_evaluation(env, policy, gamma, theta, state_values):
    """
    policy_evaluation:     evaluate policy by estimating state values
    
    @param env:            OpenAI Gym environment
    @param policy:         policy matrix containing actions and their probability in each state
    @param gamma:          discount factor
    @param theta:          the evaluation will stop once values for all states are less than the threshold
    @param state_values:   inital state values
    
    @return:               state values of the given policy
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
                    # if we reached the goal
                    if (done):                    
                        new_s += policy[s,a] * transition_prob * reward
                    else:
                        # otherwise
                        new_s += policy[s,a] * transition_prob * (reward + gamma * state_values[next_state])
        
            delta = max(delta, np.abs(new_s - state_values[s])) 
            state_values[s] = new_s
            
    return state_values
```


```python
def policy_improvement(env, policy, state_values, gamma):
    """
    policy_improvement:  improve policy
    
    @param env:          OpenAI Gym environment
    @param policy:       policy matrix containing actions and their probability in each state
    @param gamma:        discount factor
    @param state_values: the evaluation will stop once values for all states are less than the threshold
    
    @return policy_stable: flag for if policy is stable
    @return policy:        improved policy
    """
    
    policy_stable = True
    state_len = env.nS
    action_len = env.nA
    
    # for all states
    for s in range(state_len):
        # actions from current state
        old_action = np.argmax(policy[s])
        temp_array = np.zeros((action_len))
        # for all actions from current state
        for a in range(action_len):
            # get the current transitions list (U,D,L,R)
            transitions_list = env.P[s][a]
            # for all transitions from current state
            for i in transitions_list:
                # calculate new state values
                transition_prob, next_state, reward, done = i
                if (done):                    
                    temp_array[a] += transition_prob * reward
                else:
                    temp_array[a] += transition_prob * (reward + gamma * state_values[next_state])
        
        policy[s] = np.zeros((action_len))
        policy[s, np.argmax(temp_array)] = 1.
        if old_action != np.argmax(policy[s]): 
            policy_stable = False
            
    return policy_stable, policy
```


```python
def policy_iteration(env, gamma, theta):
    # initial state values
    state_values = np.zeros(n_state)

    # create a random policy
    policy = np.ones((env.nS, env.nA))/env.nA
    policy_stable = False
    
    while not policy_stable:
        # policy evaluation
        state_values = policy_evaluation(env, policy, gamma, theta, state_values)
        # policy improvement
        policy_stable, policy = policy_improvement(env, policy, state_values, gamma)
        
    return state_values, policy
```


```python
import gym

# use the frozen lake env
env = gym.make('FrozenLake-v0', is_slippery=False)

# discount factor gamma
gamma = 0.99

# intial policy: agents can take actions at equal probability
policy = np.ones((n_state, n_action))/n_action

# threshold
theta = 0.0001

# call the policy iteration method
states, policy = policy_iteration(env, gamma, theta)
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
