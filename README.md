# velodyen_start
puck 16 setting

#install about Puck16
  sudo apt-get install ros-kinetic-velodyne*
  
==========================================================================================================
1. install PCL1.8 ver.
A. Setup Prerequisites ( from https://larrylisky.com/2016/11/03/point-cloud-library-on-ubuntu-16-04-lts/ )
  sudo apt-get update
  sudo apt-get install git build-essential linux-libc-dev
  sudo apt-get install cmake cmake-gui 
  sudo apt-get install libusb-1.0-0-dev libusb-dev libudev-dev
  sudo apt-get install mpi-default-dev openmpi-bin openmpi-common  
  sudo apt-get install libflann1.8 libflann-dev
  sudo apt-get install libeigen3-dev
  sudo apt-get install libboost-all-dev
  sudo apt-get install libvtk5.10-qt4 libvtk5.10 libvtk5-dev
  sudo apt-get install libqhull* libgtest-dev
  sudo apt-get install freeglut3-dev pkg-config
  sudo apt-get install libxmu-dev libxi-dev 
  sudo apt-get install mono-complete
  sudo apt-get install qt-sdk openjdk-8-jdk openjdk-8-jre
  
B. pcl-1.8( from https://pcl.gitbook.io/tutorial/part-0/part00-chapter02 )
#Ubuntu 16 (checked!)
  wget https://github.com/PointCloudLibrary/pcl/archive/pcl-1.8.1.tar.gz
  tar zvfx pcl-1.8.1.tar.gz
#In this step, you should change the file name(pcl_pcl-1.8.1 --> pcl-1.8.1)
  cd pcl-1.8.1
  mkdir build && cd build
  cmake .. # with enhanced compiler optimizations `cmake -DCMAKE_BUILD_TYPE=Release ..`
  make -j8
  sudo make install
  
==========================================================================================================
2. Install Eigen3 & Boost 
A. Eigne3
Already installed in ROS (https://kezunlin.me/post/d97b21ee/)
BUT! We need eigen3.3 (>-3.3 version)
Downloda here --> http://eigen.tuxfamily.org/index.php?title=Main_Page
Extract to Libraries and rename Eigen3.3
  cd Libraries/Eigen3.3/
  mkdir build
  cd build/
  cmake ..
#You can see something to do next
  sudo make install
  
B. Boost

==========================================================================================================
3. libpointmatcher
(https://github.com/ethz-asl/libpointmatcher/blob/master/doc/Compilation.md)
A. Install libnabo
  mkdir ~/Libraries/
  cd ~/Libraries
  git clone git://github.com/ethz-asl/libnabo.git
  cd libnabo

  SRC_DIR=`pwd`
  BUILD_DIR=${SRC_DIR}/build
  mkdir -p ${BUILD_DIR} && cd ${BUILD_DIR}
  cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo ${SRC_DIR}
  make
  sudo make install

B. libpointmacher
  cd ~/Libraries/
  git clone git://github.com/ethz-asl/libpointmatcher.git
  cd libpointmatcher

  SRC_DIR=`pwd`
  BUILD_DIR=${SRC_DIR}/build
  mkdir -p ${BUILD_DIR} && cd ${BUILD_DIR}
  cmake -D CMAKE_BUILD_TYPE=RelWithDebInfo ${SRC_DIR}
  make

  sudo make install
  
==========================================================================================================
4. Ceres-solver ( http://ceres-solver.org/installation.html#linux )
A. dependencies
# google-glog + gflags
  sudo apt-get install libgoogle-glog-dev
# BLAS & LAPACK
  sudo apt-get install libatlas-base-dev
# SuiteSparse and CXSparse (optional)
# - If you want to build Ceres as a *static* library (the default)
#   you can use the SuiteSparse package in the main Ubuntu package
#   repository:
  sudo apt-get install libsuitesparse-dev
# - However, if you want to build Ceres as a *shared* library, you must
#   add the following PPA:
  sudo add-apt-repository ppa:bzindovic/suitesparse-bugfix-1319687
  sudo apt-get update
  sudo apt-get install libsuitesparse-dev

B. Install Ceres Solver
#Since Ubuntu 16.04 offers eigen 3.2.92 version to user, I installed 3.3.7 ver.
  cd ~/Libraries/
  git clone https://ceres-solver.googlesource.com/ceres-solver
  cd ~/Libraries/
  cd ceres-solver/
  mkdir build
  cd build/
  cmake ..

==========================================================================================================
5. YAML ( https://github.com/jbeder/yaml-cpp )
  cd ~/Libraries/
  git clone https://github.com/jbeder/yaml-cpp.git
  cd yaml-cpp/
  mkdir build
  cd build/
  cmake ..
  make -j8
  sudo make install

==========================================================================================================
==========================================================================================================
**Dual Lidar calibration
  source ~/.bashrc
  
