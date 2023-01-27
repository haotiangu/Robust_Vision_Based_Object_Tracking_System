# Robost Vision Based Object Tracking System Demo


This repository contains code for defending the black box attack for autonomous driving or flight. We embedded an attacker which attack the object localization part of the CNN object detecter. A FPRN proposed by us also has been embedded inside the package to defend this attack. The proposed FPRN make sure the vision based object tracking to move system perform normally even under the random black box attack.


Autoflight for tracking an detected object to move can be found here -> https://www.youtube.com/watch?v=E_bgRGCXYG4
Online image attack simulaiton video can be found here -> https://www.youtube.com/watch?v=mLpQ3nOqwrU
The FPRN for defending the black box attack can be found here -> https://www.youtube.com/watch?v=MOgg8s-5LVc



## Dependency

- [Ubuntu 18.04](https://releases.ubuntu.com/18.04/)
- [ROS melodic](http://wiki.ros.org/ROS/Installation)
- [Anaconda](https://www.anaconda.com/products/distribution#linux)
- [Pytorch](https://pytorch.org/get-started/locally/)
- [Airsim](https://microsoft.github.io/AirSim/airsim_ros_pkgs/)
- [Unreal Engine](https://github.com/EpicGames/UnrealEngine)
```
cd fastdvdnet
pip install -r requirements.txt
```

## Compile

You can use the following commands to download and compile the package.

```
cd ~/catkin_ws/src
git clone https://github.com/RobustFieldAutonomyLab/LeGO-LOAM.git
cd ..
catkin_make
```



## Run the package

1. Activate the ros environment:
```
conda activate ros_env
```


2: Download the file.

```
cd ~/catkin_ws/src
git clone https://github.com/RobustFieldAutonomyLab/LeGO-LOAM.git
cd ..
catkin_make
```

Source the file before running the launch package.
```
source ~/catkin_ws/devel/setup.bash
```


3. Run the launch file:
```
roslaunch tcps_image_attack autoflight.launch # object tracking to move demo
roslaunch tcps_image_attack train.launch # attack the object localization  
roslaunch tcps_image_attack train_denoiser.launch # object tracking to move when attack exist
```
