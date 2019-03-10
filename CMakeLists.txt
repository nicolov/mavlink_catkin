cmake_minimum_required(VERSION 2.8.3)
project(mavlink_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)
file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

ExternalProject_Add(mavlink_src
  # The ROS-released version includes C++ 11 support.
  URL https://github.com/mavlink/mavlink-gbp-release/archive/release/kinetic/mavlink/2019.3.3-0.tar.gz
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX:PATH=${CATKIN_DEVEL_PREFIX}
)

cs_add_library(${PROJECT_NAME} src/lib_wrap.cc)
add_dependencies(${PROJECT_NAME} mavlink_src)

cs_install()
cs_export(
  INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
)
