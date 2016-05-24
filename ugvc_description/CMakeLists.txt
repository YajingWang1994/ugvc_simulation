cmake_minimum_required(VERSION 2.8.3)
project(ugvc_description)

find_package(catkin REQUIRED COMPONENTS 
  gazebo_ros roslaunch
)


catkin_package(
  CATKIN_DEPENDS 
    gazebo_ros 
  DEPENDS 
    gazebo
)

roslaunch_add_file_check(launch)

install(
  DIRECTORY launch meshes urdf
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
