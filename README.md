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
~~4.0.1 ver. [webpage](https://webnautes.tistory.com/1030)~~ <br/>
3.2.0 ver. Follow this [opencv(3.2.0 ver.)](https://agiantmind.tistory.com/183)
  
## nav-msgs
```bash
sudo apt install ros-kinetic-nav-msgs
```
