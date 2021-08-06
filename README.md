# Task-4
Task 4: Ros Robot Navigation.

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
Write a python script that publishes to /move_base_simple/goal topic

### 1- create a package
First, we go to the directory we want, for this we will create a catkin package.

cd ~/catkin_ws/src


Finally, we create a package with "catkin_create_pkg".

catkin_create_pkg move_base_simple


### 2- write python script
we make script with command "chmod +x script.py", inside the script:

def __init__(self, goalListX, goalListY, retry, map_frame):
        self.sub = rospy.Subscriber('move_base/result', MoveBaseActionResult, self.statusCB, queue_size=10)
        self.pub = rospy.Publisher('move_base_simple/goal', PoseStamped, queue_size=10)   
        # params & variables
        self.goalListX = goalListX
        self.goalListY = goalListY
        self.retry = retry
        self.goalId = 0
        self.goalMsg = PoseStamped()
        self.goalMsg.header.frame_id = map_frame
        self.goalMsg.pose.orientation.z = 0.0
        self.goalMsg.pose.orientation.w = 1.0
        # Publish the first goal
        time.sleep(1)
        self.goalMsg.header.stamp = rospy.Time.now()
        self.goalMsg.pose.position.x = self.goalListX[self.goalId]
        self.goalMsg.pose.position.y = self.goalListY[self.goalId]
        self.pub.publish(self.goalMsg) 
        rospy.loginfo("Initial goal published! Goal ID is: %d", self.goalId) 
        self.goalId = self.goalId + 1 
