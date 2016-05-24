cmake_minimum_required(VERSION 2.8.3)
project(ugvc_gazebo)

# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS 
  rospy
  roscpp
  std_msgs
  geometry_msgs
  sensor_msgs
  gazebo_ros  
  dynamic_reconfigure
  roslaunch
)

find_package(Protobuf REQUIRED)
find_package(gazebo REQUIRED)
find_package(Boost REQUIRED COMPONENTS system)

generate_dynamic_reconfigure_options(config/ugvc_gazebo.cfg)

link_directories(${GAZEBO_LIBRARY_DIRS})
include_directories(${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS} ${GAZEBO_INCLUDE_DIRS})

roslaunch_add_file_check(launch)

message("gazebo include path: ${GAZEBO_INCLUDE_DIRS}")

catkin_package(
  CATKIN_DEPENDS 
    sensor_msgs
    gazebo_ros 
    roscpp
    dynamic_reconfigure
  DEPENDS 
    gazebo
)

catkin_add_env_hooks(kylin_gazebo
  SHELLS sh DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/env-hooks)

install(
  DIRECTORY launch worlds urdf
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
