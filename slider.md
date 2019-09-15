---
layout: slider
title: Gait Pattern Generation of SLIDER
---

[SLIDER](http://www.imperial.ac.uk/robot-intelligence/robots/slider/) is a novel bipedal walking robot with knee-less legs and has a vertical hip sliding motion. [Here](http://kormushev.com/publication/wang2018clawar/) is a more detailed description about its mechanical design. This project explores the gait pattern generation algorithm for this robot. The primary goal of this project is to modify an existing C++ code used for walking pattern generation of another robot [COMAN](https://ieeexplore.ieee.org/document/7353844) so that it can be reused for our robot SLIDER. 

The walking pattern generation process is divided into two stages. The first stage uses the linear inverted pendulum (LIP) model and accepts the reference center of mass (CoM) velocity as input to generate a semi-dynamically consistent zero moment point (ZMP) trajectory. The second stage uses this reference ZMP trajectory to generate the final gait pattern. It contains the preview controller with multibody system (MBS) included which is a more accurate description of the actual system's dynamics than considering the robot as a point mass (LIP model). The preview controller is actually solving an unconstrained linear quadratic tracking problem with receding horizon control. It is used as a dynamics filter in the second stage for the reference motion generated from the first stage.

Another feature of the C++ code is the regeneration strategy which is activated when the CoM position of the robot deviates too much from the reference. This regeneration is achieved by solving a nonlinear program (NLP) which minimizes the foot displacement and gives the optimal gait parameters for the next two consecutive steps. In our implementation, [IPOPT](https://www.coin-or.org/Ipopt/documentation/) is used as the nonlinear programming solver.

This modified C++ code is then ROSified to interact with Gazebo. The simulation result shows a quite stable walking pattern and the robot can also sidestep to recover from the push in the y direction (coronal plane) and return to the limit cycle within three steps. 

I also reimplemented the operational space controller mentioned [here](http://www.roboticsproceedings.org/rss14/p54.pdf). It solves a quadratic program (QP) at each time step based on the current state of the robot and generates the joint torques to be executed on the robot. The motion reference for this controller is still generated from the LIP model since I did not have enough time to finish programming the high-level trajectory optimization used for controlling Cassie. The code is also written in C++ and ROSified to communicate with Gazebo. [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) is used for linear algebra, [Pinocchio](https://stack-of-tasks.github.io/pinocchio/) is used for multi-body dynamics computations and [qpOASES](https://projects.coin-or.org/qpOASES) is used as the quadratic programming solver. The simulation result shows a successful torque-controlled walking pattern, though the computational speed of my implementation needs to be increased by reformulating the QP problem and using a faster QP solver if possible. 

In addition to the modification and reimplementaion of the above control algorithms, I also participated in the walking test of the real robot and proposed a geometrical method to solve the inverse kinematics of the novel ankle design, which reduces the computational time to 2 ms in MATLAB. 


[back to home](./)
