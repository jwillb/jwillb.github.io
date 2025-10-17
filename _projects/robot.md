---
title: Two-Wheeled Vision Robot
excerpt: A semi-autonomous robot built with an ESP-32 and a Raspberry Pi (In progress!)
collection: projects
---

This project is currently in progress, so this write-up is not finished.
## Background
As the current Software Co-Lead of [ARVP](/experience/arvp), I decided that I wanted to learn more about the other systems that make the robot work. What better way to do this than make my own robot? I decided to make a robot that uses two wheels for a few reasons:
1. It is cheaper than other form factors while allowing for equivalent movement.
2. There are a few examples of this on the internet, so I knew it was possible (Though my implementation is different from most of them).
3. It allows me to learn about more advanced control systems.

## Hardware
After this was decided, I needed to figure out the materials I needed. What was clear is that I needed a microcontroller, some motors, and an *inertial measurement unit* (IMU) to allow the robot to balance itself. 

I decided on the MPU6050 IMU because it is widely used and cost-effective. I went with an ESP-32 for the microcontroller because it was cheap, and had dual cores. This would allow me to run the PID balance controller on one core and the others tasks on the other core, via the FreeRTOS-based software on the ESP-32. The motors were the hardest part to figure out, since I don't really know much about motors as a CS student. Since it seemed like most batteries I could use at this size had a rated voltage of ~6-11V, I wanted a 6V motor. This is where I ran into another issue: For running autonomous tasks, the robot needs to roughly know its position. The IMU is not nearly accurate enough, so what was I supposed to do? 

The answer: Motor encoders. These are simply a magnet that measures the amount of time another magnet passes by it. Doing this lets you figure out the RPM of the motor, which lets you determine how fast the robot is moving assuming you know the wheel circumference. When you know the time, and how fast the motor is spinning, you can determine the distance that the motor has spun. Using some math, the robot can then determine where it is. Unfortunately, this had another issue: I couldn't find a motor that was both 6 volts AND had a built-in encoder (I didn't want to use an external encoder because it would greatly increase the complexity of the wire). Luckily after some searching, I managed to find motors that fit my requirements from Canada Robotix. I then bought a dual motor driver to control the robots from the microcontroller via PWM.

Check back later for updates!
## ...
