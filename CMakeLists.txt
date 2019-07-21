cmake_minimum_required(VERSION 3.5)
project(camera_driver)

SET(OpenCV_DIR /usr/local/share/OpenCV)
find_package(OpenCV REQUIRED)
find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  message_generation
  message_runtime
  roscpp
  sensor_msgs
  std_msgs
)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

catkin_package(CATKIN_DEPENDS cv_bridge image_transport message_generation roscpp sensor_msgs std_msgs
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
)

add_executable(camera_node src/camera_node.cpp)
add_dependencies(camera_node ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(camera_node ${catkin_LIBRARIES} ${OpenCV_LIBS})

add_executable(cam_test_subscriber src/cam_test_subscriber.cpp)
add_dependencies(cam_test_subscriber ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(cam_test_subscriber ${catkin_LIBRARIES} ${OpenCV_LIBS})