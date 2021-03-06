cmake_minimum_required(VERSION 2.6)
project(ssai)
set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS_RELEASE "-Wall -O3")

find_package(OpenCV REQUIRED)
find_package(Boost COMPONENTS system filesystem python REQUIRED)
find_package(PythonLibs REQUIRED)

set(inc_dirs
  /usr/local/include
  /usr/local/cuda/include
  ${CMAKE_CURRENT_SOURCE_DIR}/src
  ${OpenCV_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
  ${Boost_NumPy_INCLUDE_DIR}
  ${PYTHON_INCLUDE_DIRS}
  ${Caffe_INCLUDE_DIR}
)

set(lib_dirs
  /usr/local/lib
  ${TBB_LIBRARY_DIRS}
  ${Boost_NumPy_LIBRARY_DIR}
  ${Caffe_LIBRARY_DIR}
)

set(libs
    caffe
    glog
    leveldb
    lmdb
    gflags
    protobuf
    opencv_core
    opencv_highgui
    opencv_imgproc
    boost_system
    boost_filesystem
    boost_python
    boost_numpy
    python2.7
)
include_directories(
    ${inc_dirs}
)
link_directories(
    ${lib_dirs}
)

add_library(ssai SHARED
    src/ssai_tools.cpp
)
target_link_libraries(ssai
    ${libs}
)
set_target_properties(ssai PROPERTIES PREFIX "")

add_executable(calc_mean_stddev
    src/calc_mean_stddev.cpp
)
target_link_libraries(calc_mean_stddev
    ${libs}
)
