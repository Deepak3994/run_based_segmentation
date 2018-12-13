cmake_minimum_required(VERSION 2.8.3)
project(3D-groundplane)
find_package(catkin REQUIRED COMPONENTS
  pcl_conversions
  pcl_ros
  roscpp
  rospy
  sensor_msgs
  std_msgs
  velodyne_pointcloud
)

catkin_package(CATKIN_DEPENDS
	sensor_msgs
	velodyne_pointcloud
)

###########
## Build ##
###########

include_directories(
  ${catkin_INCLUDE_DIRS}
)

find_package(Eigen3 REQUIRED)

#SET(CMAKE_CXX_FLAGS "-std=c++11 -O2 -g -Wall ${CMAKE_CXX_FLAGS}")
SET(CMAKE_CXX_FLAGS "-std=c++11 -O2 -g -Wall ${CMAKE_CXX_FLAGS}")

link_directories(${PCL_LIBRARY_DIRS})

#Ground Plane Fitter
find_package(PCL 1.7 REQUIRED)
add_definitions(${PCL_DEFINITIONS})

add_executable(groundplanfit src/groundplanfit.cpp
)

target_include_directories(groundplanfit PRIVATE
	${PCL_INCLUDE_DIRS}
)

target_link_libraries(groundplanfit
	${catkin_LIBRARIES}
	${PCL_LIBRARIES}
)

#Scan Line Run
add_executable(scanlinerun src/scanlinerun.cpp
)

target_include_directories(scanlinerun PRIVATE
	${PCL_INCLUDE_DIRS}
)

target_link_libraries(scanlinerun
	${catkin_LIBRARIES}
	${PCL_LIBRARIES}
)

