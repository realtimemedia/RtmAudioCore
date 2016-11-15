#############################################################
# CMake file - part of the Realtime Media project
#############################################################

#############################################################
# Define minimum required CMake version
#############################################################
cmake_minimum_required(VERSION 3.2 FATAL_ERROR)

#############################################################
# Define project name
#############################################################
project(RtmAudioCore)

#############################################################
# Define sources
#############################################################
set(RtmAudioCore_SRCS
    src/librtmaudiocore_global.h
)

##########################################################
# Create library
##########################################################
add_library(RtmAudioCore ${RtmAudioCore_SRCS})
add_library(Rtm::AudioCore ALIAS RtmAudioCore)

##########################################################
# Define dependencies
##########################################################
target_link_libraries(RtmAudioCore
    PUBLIC
        Qt5::Core
)

##########################################################
# Define compile definitions
##########################################################
target_compile_definitions(RtmAudioCore
    PRIVATE
        -DRTMAUDIOCORE_LIBRARY
)

##########################################################
# Define compile features
##########################################################
target_compile_features(RtmAudioCore
    PRIVATE
)

##########################################################
# Define include directories
##########################################################
target_include_directories(RtmAudioCore
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
)

##########################################################
# Define properties
##########################################################
set_target_properties(RtmAudioCore
    PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY ${RTM_RUNTIME_OUTPUT_DIRECTORY}
        LIBRARY_OUTPUT_DIRECTORY ${RTM_LIBRARY_OUTPUT_DIRECTORY}
        ARCHIVE_OUTPUT_DIRECTORY ${RTM_ARCHIVE_OUTPUT_DIRECTORY}
    VERSION ${RTMAUDIOCORE_VERSION_STRING}
    SOVERSION ${RTMAUDIOCORE_VERSION_MAJOR}
)


##########################################################
# Define install binary location
##########################################################
install(TARGETS RtmAudioCore EXPORT RtmAudioCoreConfig
    ARCHIVE  DESTINATION lib/static
    LIBRARY  DESTINATION lib
    RUNTIME  DESTINATION bin
)

##########################################################
# Define install headers location
##########################################################
install(
    DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/src/
    DESTINATION include/RtmAudioCore
    FILES_MATCHING
        PATTERN "*.h"
        PATTERN "*_p.h" EXCLUDE
)

##########################################################
# Make the project importable from the install directory
##########################################################
install(EXPORT RtmAudioCoreConfig DESTINATION share/RtmAudioCore/cmake)

##########################################################
# Make the project importable from the build directory
##########################################################
export(TARGETS RtmAudioCore FILE RtmAudioCoreConfig.cmake)

##########################################################
# Load tests
##########################################################
add_subdirectory(test/auto)
