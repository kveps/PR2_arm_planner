cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE Debug)

rosbuild_init()
SET(CMAKE_CXX_FLAGS "-std=c++0x")

find_package(PkgConfig REQUIRED)
pkg_check_modules(SBPL REQUIRED sbpl)
include_directories(${SBPL_INCLUDE_DIRS})
link_directories(${SBPL_LIBRARY_DIRS})

find_package( PkgConfig REQUIRED)
pkg_check_modules( gsl REQUIRED gsl )

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#common commands for building c++ executables and libraries
rosbuild_add_library(egraphs src/egraph.cpp src/egraph_decomposer.cpp src/egraph_2d_grid_heuristic.cpp src/egraph_3d_grid_heuristic.cpp src/egraph_euclidean_heuristic.cpp)# src/egraph_planner.cpp src/egraphManager.cpp)
target_link_libraries(egraphs ompl ompl_app ompl_app_base ${SBPL_LIBRARIES} ${gsl_LIBRARIES})
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(test_egraphs src/test_egraphs.cpp)
#target_link_libraries(test_egraphs ompl ompl_app ompl_app_base egraphs)
