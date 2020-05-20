# Velodyen_start
puck 16 setting
## Install ros driver about Puck16
```bash
sudo apt-get install ros-kinetic-velodyne*
```
## Grouping lidar launch file
```bash
roscd velodyne_pointcloud/launch/
sudo cp VLP16_points.launch two_lidar.launch
sudo gedit two_lidar.launch
```

# 1. Install PCL1.8 ver.
## 1-A. Setup Prerequisites
Detail in [here](https://larrylisky.com/2016/11/03/point-cloud-library-on-ubuntu-16-04-lts/)
```bash
sudo apt-get update
sudo apt-get install git build-essential linux-libc-dev
sudo apt-get install cmake cmake-gui 
sudo apt-get install libusb-1.0-0-dev libusb-dev libudev-dev
sudo apt-get install mpi-default-dev openmpi-bin openmpi-common  
sudo apt-get install libflann1.8 libflann-dev
sudo apt-get install libeigen3-dev
sudo apt-get install libboost-all-dev
```
When install below, something are removed (?)
```bash
sudo apt-get install libvtk5.10-qt4 libvtk5.10 libvtk5-dev
```
```bash
sudo apt-get install libqhull* libgtest-dev
sudo apt-get install freeglut3-dev pkg-config
sudo apt-get install libxmu-dev libxi-dev 
sudo apt-get install mono-complete
sudo apt-get install qt-sdk openjdk-8-jdk openjdk-8-jre
```
  
## 1-B. pcl-1.8 download
Ubuntu 16 (checked!) <br/>
Detail in [here](https://pcl.gitbook.io/tutorial/part-0/part00-chapter02)

```bash
mkdir Library
cd Library/
wget https://github.com/PointCloudLibrary/pcl/archive/pcl-1.8.1.tar.gz
tar zvfx pcl-1.8.1.tar.gz
cd pcl-1.8.1
```
Make build folder --> cmake --> make --> sudo make install
```bashe
mkdir build && cd build
cmake .. # with enhanced compiler optimizations `cmake -DCMAKE_BUILD_TYPE=Release ..`
make -j8
sudo make install
```
#### 1-B. (Alternatives)
If the above method does not work, ollow [here](https://askubuntu.com/questions/916260/how-to-install-point-cloud-library-v1-8-pcl-1-8-0-on-ubuntu-16-04-2-lts-for)

# 2. Install Eigen3 & Boost 
## 2-A. Eigne3 (3.3.1)
Already installed in ROS, but 3.2.92 version [reference](https://kezunlin.me/post/d97b21ee/)
We need eigen3.3 (>-3.3 version)
Download [here](https://gitlab.com/libeigen/eigen/-/releases/3.3.1)
```bash
cd Libraries/eigen-3.3.1/
mkdir build
cd build/
cmake ..
```
After doing cmake you can see something to do next
```bash
sudo make install
```
## 2-B. Boost
Already installed

# 3. libpointmatcher
Compiling and Installing libpointmatcher on your Computer<br/>
Detail in [here](https://github.com/ethz-asl/libpointmatcher/blob/master/doc/Compilation.md)
## 3-A. Install libnabo
```bash
mkdir ~/Libraries/
cd ~/Libraries
git clone git://github.com/ethz-asl/libnabo.git
cd libnabo
```
```bash
SRC_DIR=`pwd`
BUILD_DIR=${SRC_DIR}/build
mkdir -p ${BUILD_DIR} && cd ${BUILD_DIR}
cmake -D CMAKE_BUILD_TYPE=RelWithDebInfo ${SRC_DIR}
make
sudo make install
```

#### Additional download
It may be needed
```bash
sudo apt-get install doxygen

sudo apt update
sudo apt install ocl-icd-opencl-dev
```

## 3-B. libpointmacher
```bash
cd ~/Libraries/
git clone git://github.com/ethz-asl/libpointmatcher.git
cd libpointmatcher
```
```bash
SRC_DIR=`pwd`
BUILD_DIR=${SRC_DIR}/build
mkdir -p ${BUILD_DIR} && cd ${BUILD_DIR}
cmake -D CMAKE_BUILD_TYPE=RelWithDebInfo ${SRC_DIR}
make
sudo make install
```

# 4. [Ceres-solver]( http://ceres-solver.org/installation.html#linux )
## 4-A. dependencies
google-glog + gflags
```bash
sudo apt-get install libgoogle-glog-dev
```
BLAS & LAPACK
```bash
sudo apt-get install libatlas-base-dev
```
SuiteSparse and CXSparse (optional)
- If you want to build Ceres as a *static* library (the default), you can use the SuiteSparse package in the main Ubuntu package repository:
```bash
sudo apt-get install libsuitesparse-dev
```
- However, if you want to build Ceres as a *shared* library, you must add the following PPA:
```bash
sudo add-apt-repository ppa:bzindovic/suitesparse-bugfix-1319687
sudo apt-get update
sudo apt-get install libsuitesparse-dev
```
## 4-B. Install Ceres Solver
Since Ubuntu 16.04 offers eigen 3.2.92 version to user, I installed 3.3.1 ver.
```bash
cd Libraries/
git clone https://ceres-solver.googlesource.com/ceres-solver
cd ceres-solver/
```
```bash
mkdir build
cd build/
cmake ..
make
sudo make install
```

# 5. [YAML]( https://github.com/jbeder/yaml-cpp )
```bash
cd ~/Libraries/
git clone https://github.com/jbeder/yaml-cpp.git
cd yaml-cpp/
```
build
```bash
mkdir build
cd build/
cmake ..
make -j8
sudo make install
``` 
# 6. opencv(3.2.0 ver.)
4.0.1 ver. [webpage](https://webnautes.tistory.com/1030) X<br/>
3.2.0 ver. Follow this [opencv(3.2.0 ver.)](https://agiantmind.tistory.com/183)
  
## nav-msgs
```bash
sudo apt install ros-kinetic-nav-msgs
```

# <Dual Lidar calibration>
```bash
source ~/.bashrc
cd catkin_ws/src/
git clone https://github.com/ram-lab/lidar_appearance_calibration.git
```
[ros-kinetic-pcl-ros](https://github.com/uzh-rpg/rpg_svo_example/issues/44)
```bash
sudo apt-get install ros-kinetic-pcl-ros
```
## Warning (openni2)
If some warning about *openni2*, please see [here](https://github.com/autowarefoundation/autoware/issues/1072)

## Modify the code
- calib_evaluation.cpp <br/>
search jjiao --> modify
- calib_preprocess.cpp <br/>
search jjiao --> modify
  
  eigen3랑 pcl-1.8 include할 때 필요한 버전들이 local에 있기 때문에 경로 설정 다시!
  
  https://snapcraft.io/install/cloudcompare/ubuntu
  sudo apt update
  sudo apt install snapd
  sudo snap install cloudcompare
  
  ======================================================================================================
  
  veloview 다운로드 (아마 이거 통해서 csv파일로 바꿔줘야할듯요..
https://www.paraview.org/veloview/
  

----------------------------------------------------------------------------------------------------------
1. Create a yaml file cfg.yaml into a fold, please follow ../data/example/top_tail/cfg.yaml to write

2. Preproces raw pointcloud to keep points with only planes. You can use the below function or CloudCompare software like this: input="pcd" output="csv"
$ rosrun lidar_appearance_calibration calib_preprocess vel_to_pcd/planes/data1_con.yaml vel_to_pcd/planes/data2_con.yaml


3. Extract planes from pointcloud
terminal 1:
roscore 먼저
terminal 2:
  cd ~/catkin_ws/src/lidar_appearance_calibration/config/
  rosrun lidar_appearance_calibration calib_plane_extraction pcd ../data/example/top_front/cfg.yaml
terminal 3:
실행하고난뒤에 rviz를 켜놓는다(위치**)
  cd ~/catkin_ws/src/lidar_appearance_calibration/config/
  rviz -d ../rviz/plane_extraction.rviz
terminal 4:
터미널 2에서 계산되어 나옴
  rostopic pub /contact/icp std_msgs/String "data: ''" 

Visualize and check the extracted plane order



rosrun pcl_ros pcd_to_pointcloud ../data/example/top_front/plane/ref_planes.pcd

---------------------------------------------------------------------------------
로스백 record
rosbag record -a -O <파일 이름>

로스백 play
rosbag play <파일 이름>.bag

$ rosrun pcl_ros bag_to_pcd room_left.bag velodyne_points vel_to_pcd/
$ rosrun pcl_ros bag_to_pcd <input_file>  <topic>         <output_directory>

----------------------------------------------------------------------
pcd2csv parser 참고
https://github.com/jacoblambert/pcd2ILCCcsv

