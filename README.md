# Treasure Hunter

# 1. Overview
This is academic project based on the orb slam 2, ros and augmented reality.
Its purpose to fly with drone and find 3D objects which have been hidden 
in the room.

# 2. Prerequisites
We have tested the project in **Ubuntu 16.04** and **Ros Kinetic**, but it should be easy to compile in other platforms. A powerful computer (e.g. i7) will ensure real-time performance and provide more stable and accurate results.
Drone model is tello dji.

## Pangolin
We use [Pangolin](https://github.com/stevenlovegrove/Pangolin) for visualization and user interface. Dowload and install instructions can be found at: https://github.com/stevenlovegrove/Pangolin.

## OpenCV
We use [OpenCV](http://opencv.org) to manipulate images and features. Dowload and install instructions can be found at: http://opencv.org. **Required at leat 2.4.3. Tested with OpenCV 2.4.11 and OpenCV 3.2**.

## Eigen3
Required by g2o (see below). Download and install instructions can be found at: http://eigen.tuxfamily.org. **Required at least 3.1.0**.

## DBoW2 and g2o (Included in Thirdparty folder)
We use modified versions of the [DBoW2](https://github.com/dorian3d/DBoW2) library to perform place recognition and [g2o](https://github.com/RainerKuemmerle/g2o) library to perform non-linear optimizations. Both modified libraries (which are BSD) are included in the *Thirdparty* folder.

## ROS 
1. install ros kinetic from here: http://wiki.ros.org/ROS/Installation
2. configure catkin workspace: http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment

# 3. Building project
if you still not created catkin workspace then do:
  1. source /opt/ros/kinetic/setup.bash
  2. mkdir -p ~/catkin_ws/src
  3. cd ~/catkin_ws
  4. catkin build (or catkin_make)
  5. source devel/setup.bash
  6. echo $ROS_PACKAGE_PATH
      if you see this line /home/<user>/catkin_ws/src:/opt/ros/kinetic/share then all is good.
  
after you've created catkin_ws, do:
  1. cd ~/catkin_ws/src
  2. git clone https://github.com/MichaelCud/orb_slam_2_ros.git
  3. git clone https://github.com/MichaelCud/tello_driver.git
  4. git clone https://github.com/MichaelCud/drone_control.git
        current python module uses "import keyboard"
        if "keyboard" module is not installed, do "pip install keyboard".
        in case you get exception "keyboard module not found" after installation, then just copy keyboard directory 
        to drone_control/scripts.
  5. sudo rosdep init
  6. rosdep update
  7. rosdep install --from-paths src --ignore-src -r -y
  8. sudo apt-get install python-catkin-tools
  9. catkin init
  10. catkin clean
  11. catkin build

# 4. Run Project
1. open terminal
2. cd ~/catkin_ws
3. source devel/setup.bash
4. turn on your tello drone and connect to drone's WiFi access point (TELLO_XXXXXX)
5. wait for connection
6. roslaunch orb_slam2_ros find_the_treasure.launch
7. if everithing is ok then you will see pangolin gui opened with image recieved from drone.

for control the drone, open another terminal:
1. cd ~/catkin_ws
2. source devel/setup.bash
3. rosrun drone_control talker.py
4. control buttons:
   w - move forward
   s - move back
   a - move left
   d - move right
   up arrow key - move up
   down arrow key - move down
   left arrow key - turn left
   right arrow key - turn right
   


