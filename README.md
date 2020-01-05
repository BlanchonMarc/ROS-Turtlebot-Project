# ROS-Turtlebot-Project


## Members 
  * SHAH Bhargav
  * PARMAR Hardiksinh
  
## Table of contents
  
  
## Introduction
 The motto of this project is to familiarise with ROS and Create the map in a certain environment and autonomously move the Robot (Turtle bot 2) to the desired location in the map where we have to scan the QR code and the detect the text. 
 
 This project is tested with Ubuntu 16.04 LTS and ROS KINETIC. The hardware we are using is a Turtle Bot 2 with a Kobuki base as our robotic hardware platform with Kinect 1 which is a RGB-D sensor. We are using ROS as a software framework.
 
 ## PreRequired packages
 
 1) Mobile Robot Configuration http://wiki.ros.org/turtlebot/Tutorials/indigo/Turtlebot%20Installation
 2) Turtlebot mangement from workstation http://wiki.ros.org/ROS/Tutorials/MultipleMachines
 
 ## Localization and Mapping 
 First we need to Install packages for Rplidar and kinect sensors into your cankin workspace in the turtlebot pc into /scr folder so for that clone this repository and follow the steps.
https://github.com/roboticslab-fr/turtlebot_vibot
```
git clone  https://github.com/roboticslab-fr/turtlebot_vibot
cd </catkin_ws>
catkin make
rospack profile
```
In this Task First, we have to create a Map using a gmapping package. The gmapping package gives laser-based SLAM      (Simultaneous Localization and Mapping), as a ROS node called slam_gmapping. Utilizing slam_gmapping, you can make a 2-D inhabitance framework map (like a structure floorplan) from a laser and posture information gathered by a versatile robot.to create the map and move the robot autonomously follow the tutorial https://github.com/roboticslab-fr/turtlebot_vibot/tree/master/turtlebot_vibot_nav

![image 1](https://github.com/bhargav011/ROS-Turtlebot-Project/blob/master/map/Screenshot%20from%202019-12-20%2013-54-05.png)

here is the image visualize after creating the map.

 
 
 
