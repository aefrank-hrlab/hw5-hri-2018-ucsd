cmake_minimum_required(VERSION 2.8.3)
project(turtlebot_survivor)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS nodelet roscpp visualization_msgs turtlebot_msgs depth_image_proc dynamic_reconfigure)
find_package(Boost REQUIRED)


generate_dynamic_reconfigure_options(cfg/Survivor.cfg)

catkin_package(
  INCLUDE_DIRS
  LIBRARIES turtlebot_survivor
  CATKIN_DEPENDS nodelet roscpp visualization_msgs turtlebot_msgs depth_image_proc dynamic_reconfigure
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
 include_directories(
    include
    ${catkin_INCLUDE_DIRS}
    ${Boost_INCLUDE_DIRS}
)

## Declare a C++ library
add_library(turtlebot_survivor
   src/survivor.cpp
 )

## Add cmake target dependencies of the library
add_dependencies(
   turtlebot_survivor
   ${catkin_EXPORTED_TARGETS}
   turtlebot_survivor_gencfg
   ${turtlebot_msgs_EXPORTED_TARGETS}
)

## Specify libraries to link a library or executable target against
 target_link_libraries(turtlebot_survivor
   ${catkin_LIBRARIES}
 )

#############
## Install ##
#############

## Mark executables and/or libraries for installation
 install(TARGETS turtlebot_survivor
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
 )

## Mark other files for installation
install(DIRECTORY launch
   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(DIRECTORY param
   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(DIRECTORY plugins
   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

## Mark executable scripts for installation
install(PROGRAMS
   scripts/switch.py
   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
