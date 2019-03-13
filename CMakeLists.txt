cmake_minimum_required(VERSION 2.4.6)
project(demo_lidar)

add_definitions(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  nav_msgs
  sensor_msgs
  roscpp
  rospy
  std_msgs
  cv_bridge
  image_transport
  OpenCV
  tf)

find_package(Eigen3 REQUIRED)
find_package(PCL REQUIRED)
find_package(OpenCV REQUIRED)

include_directories(
  include
	${catkin_INCLUDE_DIRS} 
	${EIGEN3_INCLUDE_DIR}
	${PCL_INCLUDE_DIRS})

catkin_package(
  CATKIN_DEPENDS geometry_msgs nav_msgs roscpp rospy std_msgs
  DEPENDS EIGEN3 PCL OpenCV
  INCLUDE_DIRS include
)
SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
add_subdirectory(isamlib)
link_libraries(isamlib)

add_executable(${PROJECT_NAME}featureTracking src/featureTracking.cpp)
target_link_libraries(${PROJECT_NAME}featureTracking ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable(${PROJECT_NAME}visualOdometry src/visualOdometry.cpp)
target_link_libraries(${PROJECT_NAME}visualOdometry ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable(${PROJECT_NAME}bundleAdjust src/bundleAdjust.cpp)
target_link_libraries(${PROJECT_NAME}bundleAdjust ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable(${PROJECT_NAME}processDepthmap src/processDepthmap.cpp)
target_link_libraries(${PROJECT_NAME}processDepthmap ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable(${PROJECT_NAME}stackDepthPoint src/stackDepthPoint.cpp)
target_link_libraries(${PROJECT_NAME}stackDepthPoint ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable(${PROJECT_NAME}transformMaintenance src/transformMaintenance.cpp)
target_link_libraries(${PROJECT_NAME}transformMaintenance ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable(${PROJECT_NAME}registerPointCloud src/registerPointCloud.cpp)
target_link_libraries(${PROJECT_NAME}registerPointCloud ${catkin_LIBRARIES} ${PCL_LIBRARIES} ${OpenCV_LIBS})




