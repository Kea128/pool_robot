cmake_minimum_required(VERSION 3.0.2)
project(robot_control)

# # Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)
find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  roscpp
  rospy
  sensor_msgs
  std_msgs
  quaternion
  control
  custom_msgs
)

# 查找 glog 库
find_package(glog REQUIRED)

# 查找 gflags 库
find_package(gflags REQUIRED)

catkin_package(

  # INCLUDE_DIRS include
  # LIBRARIES robot_control
  # CATKIN_DEPENDS geometry_msgs roscpp rospy sensor_msgs std_msgs
  # DEPENDS system_lib
)

include_directories(

  # include
  ${catkin_INCLUDE_DIRS}
)

# # Declare a C++ library
# add_library(${PROJECT_NAME}
# src/${PROJECT_NAME}/robot_control.cpp
# )

# add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
add_executable(sensor src/sensor.cc)

add_executable(control_service src/control_service.cc)

add_executable(control_keyboard src/control_keyboard.cc)

# add_dependencies(sensor ${PROJECT_NAME}_gencpp)
# add_dependencies(control_service ${PROJECT_NAME}_gencpp)
target_link_libraries(sensor
  ${catkin_LIBRARIES}
  glog::glog
  gflags
)

target_link_libraries(control_service
  ${catkin_LIBRARIES}
  glog::glog
  gflags
)

target_link_libraries(control_keyboard
  ${catkin_LIBRARIES}
  glog::glog
  gflags
)
