---
layout: post
title:  "DeepMind x UCL | Deep Learning Lecture 1-10 Notes 2020"
date:   2020-07-06 12:00:00
---

## Article Goal

This article contains my notes from the DeepMind x UCL Deep Learning Lectures 1-12.

# Topics
- [1. Intro to Machine Learning & AI](#1-intro-to-machine-learning-and-ai)
	- [Solving Intelligence](#solving-intelligence)
	- [What is intelligence?](#what-is-intelligence)
	- [Reinforcement Learning](#reinforcement-learning)
	- [Why use games to solve AI?](#why-use-games-to-solve-ai)
	- [Why "Deep Learning"?](#why-deep-learning)
	- [Case Study 1 AlphaGo and AlphaZero](#case-study-1-alphago-and-alphazero)
	- [Case study 2 Capture the Flag game](#case-study-2-capture-the-flag-game)
	- [Case study 3 AlphaFold](#case-study-3-alphafold)

## 1. Intro to Machine Learning & AI

Delivered by DeepMind Research Scientist and UCL Professor Thore Graepel.

### Solving Intelligence 

"A human being should be able to change a diaper, plan an invasion, butcher a hog, conn a ship, design a building, write a sonnet, balance accounts, build a wall, set a bone, comfort the dying, take orders, give orders, cooperate, act alone, solve equations, analyze a new prpblem, pitch manure, program a computer, cook a tasty meal, fight efficiently, die gallantly. Specialization is for insects." - **Robert A Heinlein (Science Fiction Author)**

### What is intelligence?

Intelligence measures an agents ability to achieve goals in a wide range of environments.

### Reinforcement Learning

General purpose framework for AI. Agent interacts with the environment. Select actions to maximize long-term reward.  Encompasses supervised and unsupervised learning as special cases. 

The combination of deep learning and reinforcement learning enables us to solve complex interactive problems in the world.

### Why use games to solve AI?

Reinforcement learning applied to Atari games where superhuman skill was achieved by the AI. Games are a bit like reinforcement learning. Designed to stimulate human intelligence. We can simulate games and learn quickly. Score associated to measure progress. 

### Why "Deep Learning"?

Deep learning made possible by: greater computational power (GPUs, TPUs), large amount of data, better understanding of algorithms and architectures.

### Case Study 1 AlphaGo and AlphaZero

"A general reinforcement learning algorithm that masters chess, shogi, and Go through self-play" - **David Silver and others.**

**AlphaGo**: There are so many different moves in any given position. 361 vertices on which you can take turns to place black and white stones to surround territory. That's where deep learning kicks in. We use two neural networks to reduce the size of the search space.

The first one we call the **policy network**. The second one is called the **value network**.

The policy network takes as input a raw goal position, it outputs a moves. The value networks tells us how good is that move.

These two neural networks give us guidance. The policy network allows us to be smart about the moves that we choose. We don't need to check out all the moves that start from this position. We can focus on the promising ones where the professional or strong go player would be likely to play and that biases the search in the right direction. Now the problem that remains is that the game tree is still very deep. A typical game of go can last 200 moves 250 moves even longer sometimes so how do we deal with that. That's where the value net comes in because we don't need to go all the way to the end of the game to observe its outcome if black wins or white wins. We can stop somewhere in the middle after a few moves and use the trained value network to give us an estimate of how good the position is for black or for white and so together the policy network and the value network reduce the size of this huge search tree and allow us to traverse it and find good plans in it.

**AlphaGo Zero or AlphaZero**: plays chess games against itself or self-play and self-learns to become stronger and stronger and discover new knowledge. 

AlphaZero at its heart, lies the following beautifully simple mantra for learning:

> Mentally play through possible future scenarios, giving priority to promising paths, whilst also considering how others are most likely to react to your actions and continuing to explore the unknown.
> 
> After reaching a state that is unfamiliar, evaluate how favourable you believe the position to be and cascade the score back through previous positions in the mental pathway that led to this point.
> 
> After you’ve finished thinking about future possibilities, take the action that you’ve explored the most.
> 
> At the end of the game, go back and evaluate where you misjudged the value of the future positions and update your understanding accordingly.


## The Convenient Properties of Go

I wanted to expand on the narrowness of AlphaGo by explicitly trying to list some of the specific properties that Go has, which AlphaGo benefits a lot from. This can help us think about what settings AlphaGo does or does not generalize to. Go is:

1.  fully  **deterministic.** There is no noise in the rules of the game; if the two players take the same sequence of actions, the states along the way will always be the same.
2.  fully  **observed.** Each player has complete information and there are no hidden variables. For example, Texas hold’em does not satisfy this property because you cannot see the cards of the other player.
3.  the action space is  **discrete.** a number of unique moves are available. In contrast, in robotics you might want to instead emit continuous-valued torques at each joint.
4.  we have access to a perfect  **simulator**  (the game itself)**,**  so the effects of any action are known exactly. This is a strong assumption that AlphaGo relies on quite strongly, but is also quite rare in other real-world problems.
5.  each episode/game is relatively  **short,**  of approximately 200 actions. This is a relatively short time horizon compared to other RL settings which may involve thousands (or more) of actions per episode.
6.  the  **evaluation**  is clear, fast and allows a lot of  **trial-and-error** experience. In other words, the agent  can experience winning/losing millions of times, which allows is to learn, slowly but surely, as is common with deep neural network optimization.
7.  there are huge  **datasets of human play**  game data available to bootstrap the learning, so AlphaGo doesn’t have to start from scratch.

### Case study 2 Capture the Flag game

Deep reinforcement learning learn to play complex multi player video games at human level. Multi-agents systems.

### Case study 3 AlphaFold

Protein folding in biology. Train neural network to learn
