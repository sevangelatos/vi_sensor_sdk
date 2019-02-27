cmake_minimum_required(VERSION 2.8.3)
project(loitor_stereo_visensor)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  cv_bridge
  image_transport
  message_generation
  sensor_msgs
)

find_package(OpenCV 3.1 REQUIRED)
find_package (Threads REQUIRED)

catkin_package(
  CATKIN_DEPENDS
  cv_bridge
  image_transport
  message_runtime
  sensor_msgs
  DEPENDS
  OpenCV
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")

include_directories(include 
${catkin_INCLUDE_DIRS})

include_directories("./include/loitor_stereo_visensor")

add_library(loitorusbcam src/loitorusbcam.cpp)
target_link_libraries(loitorusbcam loitorimu)

add_library(loitorimu src/loitorimu.cpp)

add_executable(loitor_stereo_visensor src/loitor_stereo_visensor.cpp) 
target_link_libraries(loitor_stereo_visensor ${catkin_LIBRARIES})
target_link_libraries(loitor_stereo_visensor
  loitorusbcam
  loitorimu
  usb-1.0
  Threads::Threads
  ${OpenCV_LIBRARIES})


















