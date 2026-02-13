cmake_minimum_required(VERSION 3.5)
project(common_msgs)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic -O3)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(std_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)

find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/ActuatorStatus.msg"
  "msg/CmdEcu.msg"
  "msg/CmdMotor.msg"
  "msg/ControlLog.msg"
  "msg/EcuStatus.msg"
  "msg/ImuCanData.msg"
  "msg/Imu/Acceleration.msg"
  "msg/Imu/EulerAngles.msg"
  "msg/Imu/Gnss.msg"
  "msg/Imu/GnssStatus.msg"
  "msg/Imu/Quaternion.msg"
  "msg/Imu/RateOfTurn.msg"
  "msg/Imu/UTCTime.msg"
  "msg/Imu/Velocity.msg"
  "msg/NavSatHeading.msg"
  "msg/PurePursuitLog.msg"
  "msg/RaceStatus.msg"
  "msg/ResStatus.msg"
  "msg/TrajectoryPoint.msg"
  "msg/TrajectoryPoints.msg"
  DEPENDENCIES
  std_msgs 
  geometry_msgs
  sensor_msgs
 )

ament_export_dependencies(rosidl_default_runtime)

install(FILES
  config/configuration.hpp
  DESTINATION include/${PROJECT_NAME}/${PROJECT_NAME}
)

# Install launch directory
# install(DIRECTORY
#   launch
#   scripts
#   DESTINATION share/${PROJECT_NAME}
# )

# install(FILES
#   config/car_configurations.h
#   config/configuration.hpp
#   DESTINATION include/${PROJECT_NAME}
# )

# Install config directory
# install(DIRECTORY
#   config
#   DESTINATION share/${PROJECT_NAME}
# )

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips tCMAKE_PREFIX_PATHhe linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
