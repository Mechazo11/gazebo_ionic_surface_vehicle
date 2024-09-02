cmake_minimum_required(VERSION 3.10.2 FATAL_ERROR)
# Project name
project(gazebo_maritime)
# Required packages
find_package(gz-sim9 REQUIRED)
set(GZ_SIM_VER ${gz-sim9_VERSION_MAJOR})

find_package(gz-common6 REQUIRED COMPONENTS graphics)
set(GZ_COMMON_VER ${gz-common6_VERSION_MAJOR})

find_package(gz-math7 REQUIRED)
set(GZ_MATH_VER ${gz-math7_VERSION_MAJOR})

find_package(gz-msgs11 REQUIRED)
set(GZ_MSGS_VER ${gz-msgs11_VERSION_MAJOR})

find_package(gz-transport14 REQUIRED)
set(GZ_TRANSPORT_VER ${gz-transport14_VERSION_MAJOR})

find_package(gz-plugin3 REQUIRED COMPONENTS loader register)
set(GZ_PLUGIN_VER ${gz-plugin3_VERSION_MAJOR})

find_package(gz-rendering9 REQUIRED)
set(GZ_RENDERING_VER ${gz-rendering9_VERSION_MAJOR})

find_package(gz-sensors9 REQUIRED)
set(GZ_SENSORS_VER ${gz-sensors9_VERSION_MAJOR})

find_package(gz-utils3 REQUIRED)
set(GZ_UTILS_VER ${gz-utils3_VERSION_MAJOR})

find_package(sdformat15 REQUIRED)

find_package(Eigen3 REQUIRED)

# Waves
add_library(Waves SHARED
  src/Wavefield.cc
)
target_link_libraries(Waves PUBLIC
  Eigen3::Eigen
  gz-common${GZ_COMMON_VER}::gz-common${GZ_COMMON_VER}
  gz-math${GZ_MATH_VER}
  gz-msgs${GZ_MSGS_VER}::gz-msgs${GZ_MSGS_VER}
  gz-sim${GZ_SIM_VER}::core
)
install(
  TARGETS Waves
  DESTINATION lib)

# Other plugins
list(APPEND MARITIME_GZ_PLUGINS
  PublisherPlugin
  Surface
  WaveVisual
)

foreach(PLUGIN ${MARITIME_GZ_PLUGINS})
  add_library(${PLUGIN} SHARED src/${PLUGIN}.cc)
  target_link_libraries(${PLUGIN} PUBLIC
    Eigen3::Eigen
    gz-plugin${GZ_PLUGIN_VER}::gz-plugin${GZ_PLUGIN_VER}
    gz-rendering${GZ_RENDERING_VER}::gz-rendering${GZ_RENDERING_VER}
    gz-sensors${GZ_SENSORS_VER}::gz-sensors${GZ_SENSORS_VER}
    gz-sim${GZ_SIM_VER}::core
    gz-transport${GZ_TRANSPORT_VER}::gz-transport${GZ_TRANSPORT_VER}
    gz-utils${GZ_UTILS_VER}::gz-utils${GZ_UTILS_VER}
    Waves
  )
endforeach()

install(
  TARGETS ${MARITIME_GZ_PLUGINS}
  DESTINATION lib)

#============================================================================
# Resources
install(DIRECTORY
  models
  worlds
  DESTINATION share/${PROJECT_NAME})
