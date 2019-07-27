---
layout: slider
title: SLIDER
---

## Introduction
SLIDER is a novel bipedal walking robot with knee-less legs and has a vertical hip sliding motion. [Here](http://kormushev.com/publication/wang2018clawar/) is a more detailed description about its mechanical design. My project is focused on the control algorithm for motion planning of this robot. Since the whole SLIDER project is still in progress and we are at the key stage of walking test, we cannot provide too much detailed information about this project. But, hopefully, we will finish the walking test in this summer. 

## Linear inverted pendulum and preview control
The current control algorithm we are using is a two-stage controller, where the first stage generates the centre of mass (COM) and feet trajectories using linear inverted pendulum (LIMP) model and the second stage uses preview control to refine the trajectories by considering the multi-body kinematics so that the final joint trajectory is dynamically consistent with the real robot. This part of work is about modifying the C++ code used in controlling another robot as mentioned in this [paper](https://ieeexplore.ieee.org/document/6739663). By using this algorithm, SLIDER can walk with forward speed up to 0.5 m/s in simulation.

## Online regeneration by finding the optimal gait parameters 
Based on the above walking pattern generator, we continuously checking the desired COM position with the one estimated from IMU and forward kinematics. If the deviation becomes larger than a certain tolerance, we regenerate the trajectory by solving a nonlinear program to find the optimal gait parameters to bring the robot back to limit cycle. The detailed realization can be found in this [paper](https://ieeexplore.ieee.org/document/7353844). The overall structure of this method has already been implemented and we are now in the stage of tuning the parameters in order to fit our robot model. All the methods mentioned so far have been coded in C++ and ROSified to interact with Gazebo.

## Current work
We are now mainly focusing on using trajectory optimization as a high-level controller to generate the COM and end-effector trajectories and then formulating a quadratic program to track these desired trajectories. Especially, using reduced order model and finding a convex formulation so that the algorithm can be computed fast enough to be implemented in an MPC fashion. More details coming soon.

[back to home](./)
