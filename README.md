# MARSIM: Lidar-Based UAV Simulator

Paper is available on Arxiv: https://arxiv.org/abs/2211.10716

The video is available on youtube: https://youtu.be/hiRtcq-5lN0 and 
【MARSIM: 轻量化雷达无人机仿真器】 https://www.bilibili.com/video/BV1M84y117KG

<p align="center">
  <a href="https://youtu.be/hiRtcq-5lN0" target="_blank"><img src="figures/coverfigure.png" alt="video" width="800" height="400" border="1" /></a>
</p>

<p align="center">

  <img src="figures/readme_setgoal.gif" width = "400" height = "237"/>

  <img src="figures/readme_dynobs.gif" width = "400" height = "237"/>


  <img src="figures/readme_multiuav.gif" width = "400" height = "237"/>


  <img src="figures/readme_exploration.gif" width = "400" height = "237"/>
</p>

## Update

### Ubuntu 22.04 and ROS2 are also supported in ubuntu20_ros2 branch.

Ubuntu 20.04 is also supported in ubuntu20 branch.

**Ten realistic maps (low and high resolution) have been realeased in the realease packages.**

**A new branch that merge with FUEL has been released in the fuel_ubuntu20 branch.**



## Prerequisited

### Ubuntu and ROS

Ubuntu 16.04~20.04.  [ROS Installation](http://wiki.ros.org/ROS/Installation).

Or you can do it like this: 
First, Make sure Configure your Ubuntu repositories to allow "restricted," "universe," and "multiverse.". You can read the Documentation in here [Repositories/Ubuntu](https://help.ubuntu.com/community/Repositories/Ubuntu).

#### You can check by:
```
cat /etc/apt/sources.list
```

If, the output: 

```
deb http://id.archive.ubuntu.com/ubuntu focal main restricted universe multiverse
deb http://id.archive.ubuntu.com/ubuntu focal-updates main restricted universe multiverse
deb http://id.archive.ubuntu.com/ubuntu focal-security main restricted universe multiverse
```

You are ready to go

Next, 
#### Setup your computer to accept software from packages.ros.org.
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

#### Set up Your keys:
```
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

#### Installation: 
First, make sure your Debian package index is up-to-date:
```
sudo apt udpate
```
#### Now pick how much of ROS you would like to install:
I Recommend Desktop-Full Install: Everything in Desktop plus 2D/3D simulators and 2D/3D perception packages
```
sudo apt install ros-noetic-desktop-full
```
#### Environment Setup:
You must source this script in every bash terminal you use ROS in.
```
source /opt/ros/noetic/setup.bash
```
It can be convenient to automatically source this script every time a new shell is launched. These commands will do that for you.

#### Dependencies for building packages

Up to now you have installed what you need to run the core ROS packages. To create and manage your own ROS workspaces, there are various tools and requirements that are distributed separately. For example, rosinstall is a frequently used command-line tool that enables you to easily download many source trees for ROS packages with one command.

```
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```
#### Initialize rosdep
Before you can use many ROS tools, you will need to initialize rosdep. rosdep enables you to easily install system dependencies for source you want to compile and is required to run some core components in ROS. If you have not yet installed rosdep, do so as follows.

```
sudo apt install python3-rosdep
```
Initialize rosdep
```
sudo rosdep init
rosdep update
```

#### Verification
You can verify the ROS.
```
echo $ROS_DISTRO
```

### PCL && Eigen && glfw3
##### Eigen>=3.3.4
Follow [Eigen Installation](https://eigen.tuxfamily.org/index.php?title=Main_Page).
Or, You can just do:
```
sudo apt update
sudo apt install libeigen3-dev
```
Verify:
```
ls /usr/include/eigen3/Eigen
```
##### PCL>=1.6
Follow [PCL Installation](https://pointclouds.org/). 
Or, You can just do:
```
sudo apt update
sudo apt install libpcl-dev
```

Verify:
```
pkg-config --modversion pcl_common-1.10
```

##### glfw3:
```
sudo apt-get install libglfw3-dev libglew-dev
```

### Make
```
mkdir -p marsim_ws/src
cd marsim_ws/src
git clone https://github.com/hku-mars/MARSIM.git
cd ..
catkin_make
```

## Run single drone simulation with Avia

```
source devel/setup.bash
roslaunch test_interface single_drone_avia.launch
```
Click on 3Dgoal tool on the Rviz, you can give the UAV a position command to control its flight.

For now, we provide several launch files for users, which can be found in test_interface/launch folder.

You can change the parameter in launch files to change the map and LiDAR to be simulated. The maps have been uploaded to the realease files in this repository.

```
    <arg name="map_name" value="$(find map_generator)/resource/small_forest01cutoff.pcd"/>

```

**If you want to use the GPU version of MARSIM, please set the parameter "use_gpu" to true.**

## Run single drone simulation with dynamic obstacles
```
source devel/setup.bash
roslaunch test_interface single_drone_mid360_dynobs.launch
```

## Run multiple drones simulation
```
source devel/setup.bash
roslaunch test_interface triple_drone_mid360.launch
```

## Run single drones simulation with Mid-360, without obstacle
```
source devel/setup.bash
roslaunch test_interface single_drone_mid360.launch
```