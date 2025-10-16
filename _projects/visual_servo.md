---
title: Image-Based Visual Servo
excerpt: A visual control algorithm for autonomous robotics
collection: projects
---

## Background
As my first ever 'real' project for [ARVP](/experience/arvp), I was tasked with developing a visual servo control algorithm for our secondary companion robot, Koda. See, unlike on our main robot, Koda does not have a *Doppler Velocity Logger* (DVL). What this means is that it doesn't actually know where it is when it moves, it only knows its velocity. While it does have an *Inertial Measurement Unit* (IMU), this should not be used for position information because it isn't nearly as accurate. Since we wanted Koda to be able to do some tasks, we needed a way for it to move to certain places without relying on positional data. This is where visual servoing comes in.

## IBVS Explained
Image-Based Visual Servo (which I will now abbreviate to IBVS for short) is a method of controlling the way a robot moves based on visual input. I'll go over it simply here, though I'll leave a very good resource to learn more about it [here](https://inria.hal.science/inria-00350283/document). Essentially, the key to the whole system is an **interaction matrix** that explains how the data in the image relates to the movement that the robot needs to perform.

## Basic Implementation
The way that I implemented IBVS is the node (A ROS2 data structure) is given the current corners of an object it wants to align to, along with a set of target points. It then multiplies the error between the target set and current set with the interaction matrix, which gives velocities. A small, yet important, piece of information about this is that the coordinate spaces are different. On our robot (and most others), X is forward, Y is right, and Z is down. For visual servo, Z is the forward direction, X is right, and Y is down (Think Minecraft as an example). After the coordinate spaces are switched, the velocities are sent to the velocity controller on the robot.

## Integration with ROS2
Our robots use ROS2 for IPC, and I was asked to make visual servo into an action so it could be integrated into our system properly and called by other processes. Creating an action server meant that I had to have a limit on how many iterations could be performed, because actions should only run for a finite amount of time and then returned. I also had to give feedback while the action was running, accept cancellation requests, and end the action after a certain time (I decided to set a threshold that is given when the action is called, so that the caller can decided how precise the alignment needs to be).

## Unforeseen Consequences
My code worked! In the simulator, at least. It was tested on the robot and also worked, but our robot was having lots of issues at the time. The control board was not working properly and the robot would sometimes move in completely random directions and not what was sent to it. This unfortunately led to the software leads making the decision to have visual servo only align in the robot's Y and Z axes. This was a simple change because all I had to do was zero out two columns of the interaction matrix (X and Yaw, because Roll and Pitch were already zero'd). Sadly, this meant that visual servo did not live up to its full potential at the competition. Visual servo lives on inside of our robots; I think that it will be of even greater use to us next year, at RoboSub 2026.
