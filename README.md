# Task-5
Task 5: Ros Robot Navigation.

Made Abdullah Subedar

## Task1
Using SLAM map to launch the navigation

### 1- Launch Simulation world (using code below)

-choose Models: burger, waffle, waffle_pi-
export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch


### 2- Run Navigation Node

open new terminal and run this code below

export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml


### 3- Estimate initial Pose

Up at Menu-bar; there is a button "2D Pose Estimate", click it
then go to map in RViz and click on the location where the robot in simulation that you have in Gazebo window,
and drag the arrow key to north side of the map, the robot will face in that direction.

After that, run this code below

roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

Move the robot around to draw the map more accurately

by the time you finish navigating it, press (CTRL + C) to terminate the keyboard teleoperation node.


### 4- Set Navigation Goal

Up at Menu-bar; there is a button "2D Nav Goal", click it

Click on location of the map to set Navigation goal for the robot.


## Task2

