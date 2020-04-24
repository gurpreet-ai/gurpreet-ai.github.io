---
layout: post
title:  "Deep Reinforcement Learning Environment on Ubuntu 18.04 - Deep Reinforcement Learning Series"
date:   2020-04-22 12:00:00
---


In this post, I will talk about how to setup your ubuntu machine for Deep Learning projects. 

I would recommend you have a fresh downloaded Ubuntu 18.04 OS for this tutorial.

The easiest way to get started with Deep Learning on linux (Ubuntu 18.04) is to install the Anaconda Distribution.

Step 1: Install Anaconda

1. Go to https://www.anaconda.com/distribution/
2. Download the Anaconda Linux Python 3.7 version (https://repo.anaconda.com/archive/Anaconda3-2019.07-Linux-x86_64.sh)
3. Open terminal and run cd ~/Downloads/
4. Run chmod 777 Anaconda3-2019.07-Linux-x86_64.sh
5. Run ./Anaconda3-2019.07-Linux-x86_64.sh
6. Read through the instructions and all you have to do is continue to press "Enter" until it starts to install
7. Wait until the install is complete and restart your terminal screen. Now we have install Anaconda Linux Python 3.7 version

Here is how you can update anaconda in the future:
1. To update base conda installation run: conda update conda
2. To update conda packages run: conda update anaconda
3. To list you packages: conda list

Step 2: Create a virtual environment with the name ‘pytorch’

1. Create a virtual env for your pytorch projects: conda create --name pytorch anaconda python=3.7
2. To start the env: conda activate pytorch
3. To update all the packages in your env: conda update --all

Step 3: Install PyTorch

To install PyTorch via Anaconda, use the following conda command:

1. conda install pytorch torchvision -c pytorch

Step 3: Install OpenAI Gym Package

1. git clone https://github.com/openai/gym
2. cd gym
3. pip install -e .

To Test it all:

1. Open Terminal and run python
2. Run the following code:

> import torch
> print(torch.__version__)

>import gym
print(gym.__version__)

3. If the code is successful and you see the version of both torch and gym, you have successfully installed the software required for Deep Reinforcement Learning Environment on Ubuntu 18.04.
