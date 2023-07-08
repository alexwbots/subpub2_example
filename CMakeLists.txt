cmake_minimum_required(VERSION 3.8)
project(subpub2_example)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake_python REQUIRED)
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclpy REQUIRED)

# Create Cpp executable
add_executable(publisher_exe src/Publisher.cpp)
ament_target_dependencies(publisher_exe rclcpp)
add_executable(subscriber_exe src/Subscriber.cpp)
ament_target_dependencies(subscriber_exe rclcpp)

# Install Cpp executables
install(TARGETS
  publisher_exe
  subscriber_exe
  DESTINATION lib/${PROJECT_NAME}
)

# Install Python modules
ament_python_install_package(${PROJECT_NAME})

# Install Python executables
install(PROGRAMS
  scripts/Publisher.py
  scripts/Subscriber.py
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()