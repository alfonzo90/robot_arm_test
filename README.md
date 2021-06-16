# robot_arm_test
documenting the steps I took to install the robot_arm_pkg and simulate it.

This task was implemented on an ubuntu OS version 18.04 as a VM running under virtualbox.

In order to run and simulate this project I need to install ROS and many packages it uses for 2D/3D simulation among other packages. The documentation for installing ROS is http://wiki.ros.org/melodic/Installation/Ubuntu.

```
$ roscore
```

this command is used to start the master node which starts the node network.

A catkin workspace is needed, it comes with the full installation of ROS so all I need to do build the workspace. The documentation for doing that is http://wiki.ros.org/catkin/Tutorials/create_a_workspace.

Next, I need to clone the repository https://github.com/smart-methods/arduino_robot_arm inside the src folder in the catkin workspace.
```
$ cd ~/catkin_ws/src
$ sudo apt install git
$ git clone https://github.com/smart-methods/arduino_robot_arm 
```

after that I need to install all the dependencies.
```
$ cd ~/catkin_ws
$ rosdep install --from-paths src --ignore-src -r -y
$ sudo apt-get install ros-melodic-moveit
$ sudo apt-get install ros-melodic-joint-state-publisher ros-melodic-joint-state-publisher-gui
$ sudo apt-get install ros-melodic-gazebo-ros-control joint-state-publisher
$ sudo apt-get install ros-melodic-ros-controllers ros-melodic-ros-control
```

And finally compile the package.
```
$ catkin_make
```





