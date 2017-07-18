cmake_minimum_required(VERSION 2.8.3)
project(filter)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  sensor_msgs geometry_msgs tf dynamic_reconfigure
)

generate_dynamic_reconfigure_options(
  cfg/MyStuff.cfg
)


catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES temp
#  CATKIN_DEPENDS roscpp
#  DEPENDS system_lib
)

include_directories(
# include
  ${catkin_INCLUDE_DIRS}
)

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
# add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Declare a C++ executable
## With catkin_make all packages are built within a single CMake context
## The recommended prefix ensures that target names across packages don't collide


add_executable(Mahony_filter src/Mahony_filter.cpp)
add_dependencies(Mahony_filter ${PROJECT_NAME}_gencfg)
target_link_libraries(Mahony_filter ${catkin_LIBRARIES} )



