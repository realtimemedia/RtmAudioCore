##########################################################
# CMake file - part of the  project
##########################################################


##########################################################
# Define minimum required CMake version
##########################################################
cmake_minimum_required(VERSION 3.2 FATAL_ERROR)

##########################################################
# Define path to custom CMake modules
##########################################################
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules")

#########################################################
# Define paths
##########################################################
set(RTM_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/out")
set(RTM_RUNTIME_OUTPUT_DIRECTORY "${RTM_OUTPUT_DIRECTORY}/bin")
set(RTM_LIBRARY_OUTPUT_DIRECTORY "${RTM_OUTPUT_DIRECTORY}/lib")
set(RTM_ARCHIVE_OUTPUT_DIRECTORY "${RTM_OUTPUT_DIRECTORY}/static")

#########################################################
# Define version
##########################################################
set(RTMAUDIOCORE_VERSION_MAJOR 1)
set(RTMAUDIOCORE_VERSION_MINOR 0)
set(RTMAUDIOCORE_VERSION_PATCH 0)
set(RTMAUDIOCORE_VERSION_STRING "${RTMAUDIOCORE_VERSION_MAJOR}.${RTMAUDIOCORE_VERSION_MINOR}.${RTMAUDIOCORE_VERSION_PATCH}")

##########################################################
# Define global build config
##########################################################
set(BUILD_SHARED_LIBS ON)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

##########################################################
# Define global Qt5 config
##########################################################
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

##########################################################
# Find project dependencies
##########################################################
find_package(Qt5Core NO_MODULE REQUIRED)
find_package(Qt5Test NO_MODULE REQUIRED)

##########################################################
# Include subdirectories
##########################################################
add_subdirectory(libs/libRtmAudioCore)
