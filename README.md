## FAST-LIO
**FAST-LIO** (Fast LiDAR-Inertial Odometry) is a computationally efficient and robust LiDAR-inertial odometry package. It fuses LiDAR feature points with IMU data using a tightly-coupled iterated extended Kalman filter to allow robust navigation in fast-motion, noisy or cluttered environments where degeneration occurs. Our package address many key issues:
1. Fast iterated Kalman filter for odometry optimization;
2. Automaticaly initialized at most steady environments;
3. Parallel KD-Tree Search to decrease the computation;
4. Robust feature extraction;

**Developers**

Wei Xu 徐威: Laser mapping and pose optimization

Zheng Liu 刘政: Features extraction

To know more about the details, please refer to our related paper:)

**Our related paper**: our related papers are now available on arxiv:

[FAST-LIO: A Fast, Robust LiDAR-inertial Odometry Package by Tightly-Coupled Iterated Kalman Filter](https://arxiv.org/abs/2010.08196)

**Our related video**: https://youtu.be/iYCY6T79oNU

<div align="center">
    <img src="doc/results/HKU_HW.png" width = 49% >
    <img src="doc/results/HKU_MB_001.png" width = 49% >
</div>

## 1. Prerequisites
### 1.1 **Ubuntu** and **ROS**
Ubuntu >= 18.04.

ROS    >= Melodic. [ROS Installation](http://wiki.ros.org/ROS/Installation)

### 1.2. **PCL && Eigen && openCV**
PCL    >= 1.8,   Follow [PCL Installation](http://www.pointclouds.org/downloads/linux.html).

Eigen  >= 3.3.4, Follow [Eigen Installation](http://eigen.tuxfamily.org/index.php?title=Main_Page).

OpenCV >= 3.2,   Follow [openCV Installation](https://opencv.org/releases/).

### 1.3. **livox_ros_driver**
Follow [livox_ros_driver Installation](https://github.com/Livox-SDK/livox_ros_driver).


## 2. Build
Clone the repository and catkin_make:

```
    cd ~/catkin_ws/src
    git clone https://github.com/XW-HKU/fast_lio.git
    cd ..
    catkin_make
    source devel/setup.bash
```
## 3. Directly run
### 3.1 For indoor environments and high frame-rate (such as 100hz)
Connect to your PC to Livox Avia LiDAR by following  [Livox-ros-driver installation](https://github.com/Livox-SDK/livox_ros_driver), then
```
    ....
    roslaunch fast_lio mapping_avia.launch
    roslaunch livox_ros_driver livox_lidar_msg.launch
    
```
*Remarks:*
- If you want to change the frame rate, please modify the **publish_freq** parameter in the [livox_lidar_msg.launch](https://github.com/Livox-SDK/livox_ros_driver/blob/master/livox_ros_driver/launch/livox_lidar_msg.launch) of [Livox-ros-driver](https://github.com/Livox-SDK/livox_ros_driver) before make the livox_ros_driver pakage.

### 3.2 For outdoor environments
Connect to your PC to Livox Avia LiDAR following [Livox-ros-driver installation](https://github.com/Livox-SDK/livox_ros_driver), then
```
    ....
    roslaunch fast_lio mapping_avia_outdoor.launch
    roslaunch livox_ros_driver livox_lidar_msg.launch
    
```
## 4. Rosbag Example
### 4.1 Indoor rosbag (Livox Avia LiDAR)

<div align="center"><img src="doc/results/HKU_LG_Indoor.png" width=100% /></div>

Download [avia_indoor_quick_shake_example1](https://drive.google.com/file/d/1SWmrwlUD5FlyA-bTr1rakIYx1GxS4xNl/view?usp=sharing) or [avia_indoor_quick_shake_example2](https://drive.google.com/file/d/1wD485CIbzZlNs4z8e20Dv2Q1q-7Gv_AT/view?usp=sharing) and then
```
roslaunch fast_lio mapping_avia.launch
rosbag play YOUR_DOWNLOADED.bag
```
### 4.2 High-rate rosbag (Livox Avia LiDAR with 100Hz frame-rate)

Download [high_rate_avia](https://drive.google.com/file/d/1UM6O3PRN3b730ZeuvKKT3yuOLNQuz8Yf/view?usp=sharing) and then
```
roslaunch fast_lio mapping_avia.launch
rosbag play YOUR_DOWNLOADED.bag
```
### 4.3 Outdoor rosbag (Livox Avia LiDAR)

<div align="center"><img src="doc/results/HKU_MB_002.png" width=100% /></div>

<!-- <div align="center"><img src="doc/results/mid40_outdoor.png" width=90% /></div> -->

Download [avia_hku_main building_mapping](https://drive.google.com/file/d/1GSb9eLQuwqmgI3VWSB5ApEUhOCFG_Sv5/view?usp=sharing) and then
```
roslaunch fast_lio mapping_avia_outdoor.launch
rosbag play YOUR_DOWNLOADED.bag
```

## 5.Implementation on UAV
In order to validate the robustness and computational efficiency of FAST-LIO in actual mobile robots, we build a small-scale quadrotor which can carry a Livox Avia LiDAR with 70 degree FoV and a DJI Manifold 2-C onboard computer with a 1.8 GHz Intel i7-8550U CPU and 8 G RAM, as shown in below.

<div align="center">
    <img src="doc/uav01.jpg" width=40.5% >
    <img src="doc/uav_system.png" width=57% >
</div>

## 6.Acknowledgments
Thanks for LOAM(J. Zhang and S. Singh. LOAM: Lidar Odometry and Mapping in Real-time), [Livox_Mapping](https://github.com/Livox-SDK/livox_mapping) and [Loam_Livox](https://github.com/hku-mars/loam_livox).
