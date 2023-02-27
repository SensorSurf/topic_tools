cmake_minimum_required(VERSION 3.8)
project(topic_tools)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake_auto REQUIRED)
ament_auto_find_build_dependencies()

ament_auto_add_library(throttle_node SHARED
  src/throttle_node.cpp
  src/tool_base_node.cpp
)
target_compile_definitions(throttle_node PRIVATE "TOPIC_TOOLS_BUILDING_LIBRARY")

rclcpp_components_register_nodes(throttle_node "topic_tools::ThrottleNode")

ament_auto_add_executable(throttle
  src/throttle.cpp
)

target_link_libraries(throttle
  throttle_node
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_auto_package(
  INSTALL_TO_SHARE
    launch
)
