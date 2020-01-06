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
 2) Turtlebot mangement from we http://wiki.ros.org/ROS/Tutorials/MultipleMachines
 
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

after that, we created the launch file which shows the initial position of our robot into the map after we another two launch files that go to the goal position 1 and 2 where our QR code will be there so for this launch files we set the coordinates to find the goal position. the files are located into the turtlebot pc /ros_turtlebot/ros/kinetic/catkin_ws/src/turtlebot_vibot/turtlebot_vibot_nav/launch.
the launch file of first goal position show in below. 

```
<launch>
		<!--Here we give a first goal position command to the turtlebot -->
	<node name="goal_pose" pkg="rostopic" type="rostopic" args="pub /move_base_simple/goal geometry_msgs/PoseStamped '{ header: {stamp: now, frame_id: 'map'}, pose: { position: {x: -0.947343051434, y: -4.51226091385, z: 0.000}, orientation: {x: 0.000, y: 0.000, z: -0.863717802108, w: 0.503975751721}}}'"/> 
	
</launch>
```

## Computer Vision

for the Qr detection, we use pyzbar and OpenCV library. Here we use simple code using this library that scans the code and shows the result. 
QR code contains three types of data like type, data, and location moreover in the python code we use the CV_bridge for converting OpenCV image into ros image.  CvBridge is a ROS library that provides an interface between ROS and OpenCV. CvBridge can be found in the cv_bridge package in the vision_opencv stack. 
Here we saw below the launch file that launches our python file to detect the QR code and open the RGB Kinect camera. this file contains CV_bridge that convert into opecv image into ros image. python file located in /ROS Desktop/ros/kinetic/catkin_ws/src/rbx1/rbx1_vision/nodes
```
<launch>
  <node pkg="rbx1_vision" name="cv_bridge_demo" type="cv_hardik.py" output="screen">
    <remap from="input_rgb_image"   to="/camera/rgb/image_rect_color" />
    <remap from="input_depth_image" to="/camera/depth_registered/image_raw" />
  </node>
  
</launch>
```

## step to run project 

1) Connect to turtlebot from the workstation
```
ssh turtlebot@192.168.0.100
```
2) To start the TurtleBot with RP-LiDAR on the Turtlebot laptopt 
```
roslaunch turtlebot_vibot_bringup minimal_rplidar.launch
```
3) Start the Kinect on the Turtlebot laptop.
```
roslaunch turtlebot_vibot_bringup 3dsensor_rplidar.launch
```
4) Start amcl_demo (turtlebot laptop)
```
roslaunch turtlebot_vibot_nav amcl_demo_rplidar.launch map_file:=...ABSOLUTE_PATH/catkin_ws/src/turtlebot_vibot/turtlebot_vibot_nav/maps/my_map.yaml
```
5) lauch .py file for Qr code detection(workstation)
```
roslaunch rbx1_vision cv_hardik.launch
```
6) rvis launch (workstation)
 ```
 roslaunch turtlebot_rviz_launchers view_navigation.launch --screen
 ```
 7) launch file for intial position to goal 1 position (turtlebot)
 ```
 roslaunch turtlebot_vibot_nav mscv_goal1.launch
 ```
 8) launch file for goal 1 position to goal 2 positio (turtlebot)
 ```
 roslaunch turtlebot_vibot_nav mscv_goal2.launch
 ```
 
 ## VIDEO
 https://www.youtube.com/watch?v=nKyroUsNLjs&feature=youtu.be
 
 
