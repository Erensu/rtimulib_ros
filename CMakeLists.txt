cmake_minimum_required(VERSION 2.8.3)
project(rtimulib_ros)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
)

find_library(RTIMULib libRTIMULib.so)

catkin_package(
#  CATKIN_DEPENDS roscpp sensor_msgs
#  DEPENDS
#  INCLUDE_DIRS "."
#  LIBRARIES ${PROJECT_NAME}
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_executable(rtimulib_node src/rtimulib_ros.cpp)

target_link_libraries(rtimulib_node
  ${catkin_LIBRARIES}
  RTIMULib
)

#############
## Install ##
#############

install(TARGETS rtimulib_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch config
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
