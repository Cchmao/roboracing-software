cmake_minimum_required(VERSION 2.8.3)
project(rr_platform)

set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

## Find catkin macros and libraries
find_package(
        catkin REQUIRED COMPONENTS
        gencpp
        genpy
        roscpp
        rospy
        std_msgs
        sensor_msgs
        cv_bridge
        pcl_ros
        sick_tim
        laser_geometry
        image_transport
        std_msgs
        message_generation
        geometry_msgs
)

find_package(OpenCV REQUIRED)
find_package(PCL REQUIRED filters)

set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")

## Generate messages in the 'msg' folder
add_message_files(
        FILES
        speed.msg
        steering.msg
)

## Generate added messages and services with any dependencies listed here
generate_messages(
        DEPENDENCIES
        std_msgs
        geometry_msgs
)

catkin_package(
        INCLUDE_DIRS include
        CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
        DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(
        include
        ${PCL_INCLUDE_DIRS}
        ${catkin_INCLUDE_DIRS}
        ${OpenCV_INCLUDE_DIRS}
        ${EIGEN_INCLUDE_DIRS}
)

add_subdirectory(src/joystick)
add_subdirectory(src/motor_relay_node)
