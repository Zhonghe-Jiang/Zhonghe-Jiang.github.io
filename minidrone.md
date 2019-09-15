---
layout: minidrone
title: Line Following Drone
---

Our team participated in MathWorks Minidrone Competition 2019 UK. This student competition aims at designing a line follower algorithm for a minidrone using the latest features from Simulink. 

The image processing is achieved by Computer Vision Toolbox. Since the path in the simulation is always red, we only extract the red component of the raw RGB image which is then pre-processed by morphological erosion and dilation. Next, we pad the image and detect the corners using Harris Corner Detector, which gives the location of each vertex of the path. A large sensitivity factor is used in corner detection to eliminate the noisy vertices during turning. The landing circular marker is found using circular Hough transform. 

The heuristic path planning strategy is based on the information of the vertices and is implemented as a finite state machine using Stateflow. The basic idea can be summarised below. Normally, the drone keeps moving forward and tries to keep the centre of the vertices at the middle of the image. This achieved by a proportional feedback with a small P gain. When the drone finds the corner by detecting more than five vertices, the feedback is off and it will fly to the centre of the inner vertices. It then keeps turning until the centre of the vertices on the upper bound of the image reaches the middle. After finding the new path, it simply keeps flying forward with feedback on.

[back to home](./)
