cmake_minimum_required(VERSION 2.8.3)
project(lslidar_c16_decoder)

add_definitions(-std=c++0x)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  pluginlib
  sensor_msgs
  pcl_ros
  pcl_conversions
  lslidar_c16_msgs
  nodelet
)
find_package(Boost REQUIRED)


catkin_package(
  INCLUDE_DIRS include
#  LIBRARIES lslidar_c16_decoder
  CATKIN_DEPENDS
    roscpp sensor_msgs pluginlib nodelet
    pcl_ros pcl_conversions
    lslidar_c16_msgs
  DEPENDS
    Boost
)

include_directories(
  include
  ${Boost_INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
)

link_directories(
  ${catkin_LIBRARY_DIRS}
)

# Lslidar C16 Decoder
add_library(lslidar_c16_decoder
  src/lslidar_c16_decoder.cpp
)
target_link_libraries(lslidar_c16_decoder
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
)
add_dependencies(lslidar_c16_decoder
  ${${PROJECT_NAME}_EXPORTED_TARGETS}
  ${catkin_EXPORTED_TARGETS}
)

# Lslidar C16 Decoder node
add_executable(lslidar_c16_decoder_node
  src/lslidar_c16_decoder_node.cpp
)
target_link_libraries(lslidar_c16_decoder_node
  lslidar_c16_decoder
  ${catkin_LIBRARIES}
)
add_dependencies(lslidar_c16_decoder_node
  ${${PROJECT_NAME}_EXPORTED_TARGETS}
  ${catkin_EXPORTED_TARGETS}
)

# Lslidar N301 Decoder nodelet
add_library(lslidar_c16_decoder_nodelet
  src/lslidar_c16_decoder_nodelet.cpp
)
target_link_libraries(lslidar_c16_decoder_nodelet
  lslidar_c16_decoder
  ${catkin_LIBRARIES}
)
add_dependencies(lslidar_c16_decoder_nodelet
  ${${PROJECT_NAME}_EXPORTED_TARGETS}
  ${catkin_EXPORTED_TARGETS}
)


# install(TARGETS lslidar_c16_decoder_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

# install(DIRECTORY launch
#         DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )
