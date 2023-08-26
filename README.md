# TANGO-ESRGAN

**TANGO-ESRGAN** is developed to defend against the white-box attack of vision based object tracking system. It contains the online image restoration CNN TANGO-ESRGAN, the real-time object detection and localization CNN(YOLO 5.6.1), and the object tracking to move controller. 

**News**: 

- __Mar 13, 2021__: Code for fast autonomous exploration is available now! Check this [repo](https://github.com/HKUST-Aerial-Robotics/FUEL) for more details.

- __Oct 20, 2020__: Fast-Planner is extended and applied to fast autonomous exploration. Check this [repo](https://github.com/HKUST-Aerial-Robotics/FUEL) for more details.

__Authors__: [Haotian Gu](http://sysu-star.com) and [Hamid Jafarnejad Sani](https://www.stevens.edu/profile/hjafarne) from the [SIT Safe Autonomous System Lab](https://saslabstevens.github.io/).
<!-- - __B-spline trajectory optimization guided by topological paths__:
<p align="center">
  <img src="https://github.com/HKUST-Aerial-Robotics/TopoTraj/blob/master/files/icra20_1.gif" width = "420" height = "237"/>
  <img src="https://github.com/HKUST-Aerial-Robotics/TopoTraj/blob/master/files/icra20_2.gif" width = "420" height = "237"/>
</p> -->

<p align="center">
  <img src="files/raptor1.gif" width = "400" height = "225"/>
  <img src="files/raptor2.gif" width = "400" height = "225"/>
  <img src="files/icra20_2.gif" width = "400" height = "225"/>
  <img src="files/ral19_2.gif" width = "400" height = "225"/>
  <!-- <img src="files/icra20_1.gif" width = "320" height = "180"/> -->
</p>

Complete videos: 
[video1](https://www.youtube.com/watch?v=E_bgRGCXYG4),
[video2]([https://www.youtube.com/watch?v=YcEaFTjs-a0](https://www.youtube.com/watch?v=mLpQ3nOqwrU)), 
[video3]([https://www.youtube.com/watch?v=toGhoGYyoAY](https://www.youtube.com/watch?v=MOgg8s-5LVc)). 
Video 1 is for Autoflight For Tracking an Detected Object To Move. Video 2 is for Online Image Attack Simulation.Video 3 is the TANGO-ESRGAN to Defend the Adaptive White Box Attack.

Demonstrations about this work have been reported on the ICRA 2023: [page1](https://spectrum.ieee.org/automaton/robotics/robotics-hardware/video-friday-nasa-lemur-robot), [page2](https://spectrum.ieee.org/automaton/robotics/robotics-hardware/video-friday-india-space-humanoid-robot),
[page3](https://spectrum.ieee.org/automaton/robotics/robotics-hardware/video-friday-soft-exoskeleton-glove-extra-thumb) (search for _HKUST_ in the pages).

To run this project in minutes, check [Quick Start](#1-Quick-Start). Check other sections for more detailed information.

Please kindly star :star: this project if it helps you. We take great efforts to develope and maintain it :grin::grin:.






## Table of Contents

* [Quick Start](#1-Quick-Start)
* [Dependency](#2-Dependency)
* [Algorithms and Papers](#3-Algorithms-and-Papers)
* [Setup and Config](#4-Setup-and-Config)
* [Run Simulations](#5-run-simulations)
* [Use in Your Application](#6-use-in-your-application)
* [Updates](#7-updates)
* [Known issues](#known-issues)



## 1. Quick Start


Activate the ros environment:
```
  conda activate ros_env
```

The project has been tested on Ubuntu 18.04(ROS Melodic). Take Ubuntu 18.04 as an example, run the following commands to setup:

```
  cd ${YOUR_WORKSPACE_PATH}/src
  git clone https://github.com/HKUST-Aerial-Robotics/Fast-Planner.git
```

Install the dependent software of the TANGO-ESRGAN and YOLO 5.6.1

```
  cd fastdvdnet
  pip install -r requirements.txt
```

Compliling them:
```
  cd ${YOUR_WORKSPACE_PATH} 
  catkin_make
```

You may check the detailed [instruction](#3-setup-and-config) to setup the project. 
After compilation you can run a static object tracking demo: 

```
  source devel/setup.bash && roslaunch tcps_image_attack autoflight.launch # object tracking to move demo
```
run a dynamic object tracking demo: 
```
  source devel/setup.bash && roslaunch tcps_image_attack autodriving.launch # object tracking to move demo
```

Run the online adaptive white-box attack of static object tracking case and its corresponding defencing algorithm:
```
  roslaunch tcps_image_attack train.launch # attack the object localization  
  roslaunch tcps_image_attack train_denoiser.launch # object tracking to move when attack exist
```
Run the online adaptive white-box attack of dynamic object tracking case and its corresponding defencing algorithm:
```
  roslaunch tcps_image_attack train_w_car.launch # attack the object localization  
  roslaunch tcps_image_attack train_denoiser_car.launch # object tracking to move when attack exist
```

## 2. Dependency

* [Ubuntu 18.04](https://releases.ubuntu.com/18.04/)
* [ROS melodic](http://wiki.ros.org/ROS/Installation)
* [Anaconda](https://www.anaconda.com/products/distribution#linux)
* [Pytorch](https://pytorch.org/get-started/locally/)
* [Airsim](https://microsoft.github.io/AirSim/airsim_ros_pkgs/)
* [Unreal Engine](https://github.com/EpicGames/UnrealEngine)
* [Nvidia Driver 495.29.05](https://www.nvidia.com/download/driverResults.aspx/181159/en-us/)
* [CUDA 11.3](https://developer.nvidia.com/cuda-11.3.0-download-archive)
* [CUDNN 8.2.1](https://developer.nvidia.com/rdp/cudnn-archive)

Please follow the tutorial in Wiki to configure the [simulation environment](https://github.com/haotiangu/Robost_Vision_Based_Object_Tracking_System_Demo/wiki/The-General-Configuring-Tutorial-of-The-Simulation-Environment).
## 3. Algorithms and Papers

The project contains a collection of robust and computationally efficient algorithms for quadrotor fast flight:
* Kinodynamic path searching
* B-spline-based trajectory optimization
* Topological path searching and path-guided optimization
* Perception-aware planning strategy (to appear)

These methods are detailed in our papers listed below. 

Please cite at least one of our papers if you use this project in your research: [Bibtex](files/bib.txt).

- [__Robust and Efficient Quadrotor Trajectory Generation for Fast Autonomous Flight__](https://ieeexplore.ieee.org/document/8758904), Boyu Zhou, Fei Gao, Luqi Wang, Chuhao Liu and Shaojie Shen, IEEE Robotics and Automation Letters (**RA-L**), 2019.
- [__Robust Real-time UAV Replanning Using Guided Gradient-based Optimization and Topological Paths__](https://arxiv.org/abs/1912.12644), Boyu Zhou, Fei Gao, Jie Pan and Shaojie Shen, IEEE International Conference on Robotics and Automation (__ICRA__), 2020.
- [__RAPTOR: Robust and Perception-aware Trajectory Replanning for Quadrotor Fast Flight__](https://arxiv.org/abs/2007.03465), Boyu Zhou, Jie Pan, Fei Gao and Shaojie Shen, IEEE Transactions on Robotics (__T-RO__). 


All planning algorithms along with other key modules, such as mapping, are implemented in __fast_planner__:

- __plan_env__: The online mapping algorithms. It takes in depth image (or point cloud) and camera pose (odometry) pairs as input, do raycasting to update a probabilistic volumetric map, and build an Euclidean signed distance filed (ESDF) for the planning system. 
- __path_searching__: Front-end path searching algorithms. 
  Currently it includes a kinodynamic path searching that respects the dynamics of quadrotors.
  It also contains a sampling-based topological path searching algorithm to generate multiple topologically distinctive paths that capture the structure of the 3D environments. 
- __bspline__: A implementation of the B-spline-based trajectory representation.
- __bspline_opt__: The gradient-based trajectory optimization using B-spline trajectory.
- __active_perception__: Perception-aware planning strategy, which enable to quadrotor to actively observe and avoid unknown obstacles, to appear in the future.
- __plan_manage__: High-level modules that schedule and call the mapping and planning algorithms. Interfaces for launching the whole system, as well as the configuration files are contained here.

Besides the folder __fast_planner__, a lightweight __uav_simulator__ is used for testing.


## 4. Setup and Config

### Prerequisites

1. Our software is developed and tested in Ubuntu 16.04(ROS Kinetic) and 18.04(ROS Melodic). Follow the documents to install [Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu) or [Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu) according to your Ubuntu version.
   
2. We use [**NLopt**](https://nlopt.readthedocs.io/en/latest/NLopt_Installation) to solve the non-linear optimization problem. The __uav_simulator__ depends on the C++ linear algebra library __Armadillo__. The two dependencies can be installed by the following command, in which `${ROS_VERSION_NAME}` is the name of your ROS release.
``` 
sudo apt-get install libarmadillo-dev ros_${ROS_VERSION_NAME}_nlopt
```



### Build on ROS

After the prerequisites are satisfied, you can clone this repository to your catkin workspace and catkin_make. A new workspace is recommended:

```
  cd ${YOUR_WORKSPACE_PATH}/src
  git clone https://github.com/HKUST-Aerial-Robotics/Fast-Planner.git
  cd ../
  catkin_make
```

If you encounter problems in this step, please first refer to existing __issues__, __pull requests__ and __Google__ before raising a new issue.

Now you are ready to [run a simulation](#4-run-simulations).

### Use GPU Depth Rendering (can be skipped optionally)

This step is not mandatory for running the simulations. However, if you want to run the more realistic depth camera in __uav_simulator__, installation of [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit) is needed. Otherwise, a less realistic depth sensor model will be used.

 The **local_sensing** package in __uav_simulator__ has the option of using GPU or CPU to render the depth sensor measurement. By default, it is set to CPU version in CMakeLists:
 
 ```
 set(ENABLE_CUDA false)
 # set(ENABLE_CUDA true)
 ```
However, we STRONGLY recommend the GPU version, because it generates depth images more like a real depth camera.
To enable the GPU depth rendering, set ENABLE_CUDA to true, and also remember to change the 'arch' and 'code' flags according to your graphics card devices. You can check the right code [here](https://github.com/tpruvot/ccminer/wiki/Compatibility).

```
    set(CUDA_NVCC_FLAGS 
      -gencode arch=compute_61,code=sm_61;
    ) 
``` 
For installation of CUDA, please go to [CUDA ToolKit](https://developer.nvidia.com/cuda-toolkit)

## 5. Run Simulations

Run [Rviz](http://wiki.ros.org/rviz) with our configuration firstly:

```
  <!-- go to your workspace and run: -->
  source devel/setup.bash
  roslaunch plan_manage rviz.launch
```

Then run the quadrotor simulator and __Fast-Planner__. 
Several examples are provided below:

### Kinodynamic Path Searching & B-spline Optimization

In this method, a kinodynamic path searching finds a safe, dynamically feasible, and minimum-time initial trajectory in the discretized control space. 
Then the smoothness and clearance of the trajectory are improved by a B-spline optimization.
To test this method, run:

```
  <!-- open a new terminal, go to your workspace and run: -->
  source devel/setup.bash
  roslaunch plan_manage kino_replan.launch
```

Normally, you will find the randomly generated map and the drone model in ```Rviz```. At this time, you can trigger the planner using the ```2D Nav Goal``` tool. When a point is clicked in ```Rviz```, a new trajectory will be generated immediately and executed by the drone. A sample is displayed below:

<!-- add some gif here -->
 <p id="demo1" align="center">
  <img src="files/ral19_3.gif" width = "480" height = "270"/>
 </p>

Related algorithms are detailed in [this paper](https://ieeexplore.ieee.org/document/8758904).



### Topological Path Searching & Path-guided Optimization

This method features searching for multiple trajectories in distinctive topological classes. Thanks to the strategy, the solution space is explored more thoroughly, avoiding local minima and yielding better solutions.
Similarly, run:

```
  <!-- open a new terminal, go to your workspace and run: -->
  source devel/setup.bash
  roslaunch plan_manage topo_replan.launch
```

then you will find the random map generated and can use the ```2D Nav Goal``` to trigger the planner:

<!-- add some gif here -->
 <p align="center">
  <img src="files/icra20_3.gif" width = "480" height = "270"/>
 </p>

Related algorithms are detailed in [this paper](https://arxiv.org/abs/1912.12644).


### Perception-aware Replanning

The code will be released after the publication of [associated paper](https://arxiv.org/abs/2007.03465).


## 6. Use in Your Application

If you have successfully run the simulation and want to use __Fast-Planner__ in your project,
please explore the files kino_replan.launch or topo_replan.launch.
Important parameters that may be changed in your usage are contained and documented.

Note that in our configuration, the size of depth image is 640x480. 
For higher map fusion efficiency we do downsampling (in kino_algorithm.xml, skip_pixel = 2).
If you use depth images with lower resolution (like 256x144), you might disable the downsampling by setting skip_pixel = 1. Also, the _depth_scaling_factor_ is set to 1000, which may need to be changed according to your device.

Finally, for setup problem, like compilation error caused by different versions of ROS/Eigen, please first refer to existing __issues__, __pull request__, and __Google__ before raising a new issue. Insignificant issue will receive no reply.


## 7. Updates

- __Oct 20, 2020__: Fast-Planner is extended and applied to fast autonomous exploration. Check this [repo](https://github.com/HKUST-Aerial-Robotics/FUEL) for more details.
  
- __July 5, 2020__: We will release the implementation of paper: _RAPTOR: Robust and Perception-aware Trajectory Replanning for Quadrotor Fast Flight_ (submitted to TRO, under review) in the future.

- __April 12, 2020__: The implementation of the ICRA2020 paper: _Robust Real-time UAV Replanning Using Guided Gradient-based Optimization and Topological Paths_ is available.

- __Jan 30, 2020__: The volumetric mapping is integrated with our planner. It takes in depth image and camera pose pairs as input, do raycasting to fuse the measurements, and build a Euclidean signed distance field (ESDF) for the planning module.

## Known issues

### Compilation issue

When running this project on Ubuntu 20.04, C++14 is required. Please add the following line in all CMakelists.txt files:

```
set(CMAKE_CXX_STANDARD 14)
```

### Unexpected crash

If the planner dies after triggering a 2D Nav Goal, it is possibly caused by the ros-nlopt library. In this case, we recommend to uninstall it and [install nlopt following the official document](https://nlopt.readthedocs.io/en/latest/NLopt_Installation/). Then in the [CMakeLists.txt of bspline_opt package](https://github.com/HKUST-Aerial-Robotics/FUEL/blob/main/fuel_planner/bspline_opt/CMakeLists.txt), change the associated lines to link the nlopt library:

```
find_package(NLopt REQUIRED)
set(NLopt_INCLUDE_DIRS ${NLOPT_INCLUDE_DIR})

...

include_directories( 
    SYSTEM 
    include 
    ${catkin_INCLUDE_DIRS}
    ${Eigen3_INCLUDE_DIRS} 
    ${PCL_INCLUDE_DIRS}
    ${NLOPT_INCLUDE_DIR}
)

...

add_library( bspline_opt 
    src/bspline_optimizer.cpp 
    )
target_link_libraries( bspline_opt
    ${catkin_LIBRARIES} 
    ${NLOPT_LIBRARIES}
    # /usr/local/lib/libnlopt.so
    )  

```

## Acknowledgements
  We use **NLopt** for non-linear optimization.

## Licence
The source code is released under [GPLv3](http://www.gnu.org/licenses/) license.


## Disclaimer
This is research code, it is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of merchantability or fitness for a particular purpose.
