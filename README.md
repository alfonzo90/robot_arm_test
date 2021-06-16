# robot_arm_test
documenting the steps I took to install the robot_arm_pkg and simulate it

This task was implemented on an ubuntu OS version 18.04 as a VM running under virtualbox

In order to run and simulate this project I need to install ROS and many packages it uses for 2D/3D simulation among other packages. The documentation for installing ROS is http://wiki.ros.org/melodic/Installation/Ubuntu

Firstly, to start the master node input

```
$ roscore
```

## building the catkin workspace
A catkin workspace is needed, it comes with the full installation of ROS so all I need to do build the workspace. The documentation for doing that is http://wiki.ros.org/catkin/Tutorials/create_a_workspace

Next, I need to clone the repository https://github.com/smart-methods/arduino_robot_arm inside the src folder in the catkin workspace

```
$ cd ~/catkin_ws/src
$ sudo apt install git
$ git clone https://github.com/smart-methods/arduino_robot_arm 
```

after that I need to install all the dependencies

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

## RViz simulation
Now I have a working simulation, and by launching the simulator

```
$ roslaunch robot_arm_pkg check_motors.launch
```

The simulation on RViz is working and I can control the arm using the joint_state_publisher gui

### default position
![VirtualBoxVM_R54W0t2WmC](https://user-images.githubusercontent.com/25144777/122289734-b7299180-cefb-11eb-8529-0bb319e0b993.png)

### randomized position
![VirtualBoxVM_XS7juWuZsH](https://user-images.githubusercontent.com/25144777/122290101-1687a180-cefc-11eb-8302-df8a38947e30.png)

## RViz & gazebo synchronization

Normally when running RViz and gazebo side by side, changes made on RViz through the joint_state_publisher gui don't affect the simulation running on gazebo, so I need to synchronize them. A python script is provided in the robot_arm_pkg by smart-methods

First ill launch the robot arm simulation on RViz and gazebo

```
$ roslaunch robot_arm_pkg check_motors.launch
$ roslaunch robot_arm_pkg check_motors_gazebo.launch
```

Before running the synchronization script I need to give it execution permissions

```
$ cd catkin/src/arduino_robot_arm/robot_arm_pkg/scripts
$ sudo chmod +x joint_states_to_gazebo.py

```

And finally run the synchronization script

```
$ rosrun robot_arm_pkg joint_states_to_gazebo.py
```

### default position
![VirtualBoxVM_dB1r2w11jl](https://user-images.githubusercontent.com/25144777/122296784-7897d500-cf03-11eb-91da-6d52f054724b.png)

### randomized position
![VirtualBoxVM_Dfz4pIUEzN](https://user-images.githubusercontent.com/25144777/122296806-82213d00-cf03-11eb-9acd-6cdedc89f472.png)

they only look different because the angle the arm is viewed from is different

## MoveIt!

To start or open an existing MoveIt project and manipulate the configurations by inputting

```
$ roslaunch moveit_setup_assistant setup_assistant.launch
```

For the sake of the robot_arm there already exist simulations that can be launched directly running on RViz and gazebo

```
$ roslaunch moveit_pkg demo.launch
$ roslaunch moveit_pkg demo_gazebo.launch
```


