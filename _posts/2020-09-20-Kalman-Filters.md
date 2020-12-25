---
layout: post
title:  "Kalman Filters"
date:   2020-09-20 12:00:00
---

I decided to learn the kalman filters from the MATLAB Tech Talks. This is a really important method in statistics and control theory.

Kalman filters is named after Rudolf Kalman. It is an optimal estimation algorithm that predicts a parameter of interest such as location, speed, and direction in the presence of noise and measurements. They are used to find the parameter of interest that can not be measured directly, but an indirect measurement is available. They are also used to find the best estimate of states by combining measurements from various sensors in the presence of noise.

Common applications of Kalman Filters include:
 - Guidance Systems (missile guidance)
 - Navigation and control systems
 - Computer vision systems
 - Signal processing

There are few variations of Kalman Filters which depends on the system being linear or non-linear. 

| State Estimator | Model | Assumed Distribution | Computational Cost |
|--|--|--|--|
| Kalman Filter (KF) | Linear | Gaussian | Low |
| Extended Kalman Filter (EKF) | Locally Linear | Gaussian | Low |
| Unscented Kalman Filter (KF) | Nonlinear | Gaussian | Medium |
| Particle Filter (KF) | Nonlinear | Non-Gaussian | High |