cmake_minimum_required(VERSION 2.8.4 FATAL_ERROR)

cmake_policy(SET CMP0002 NEW)
cmake_policy(SET CMP0003 NEW)
cmake_policy(SET CMP0011 NEW)

# The project and cmake vars must only be defined in case that only the base
# filter should be build.
if(NOT AADC_BUILD_ALL_IN_ONE)
    # define a project name
    project(aadc_user)

    # CMAKE_BUILD_TYPE is empty on Unix systems, but needed by ADTF. Otherwise the ADTF libs
    # can't be found and linked.
    if(UNIX AND NOT CMAKE_BUILD_TYPE)
        set(CMAKE_BUILD_TYPE RelWithDebInfo CACHE STRING
                "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel."
                FORCE)
    endif(UNIX AND NOT CMAKE_BUILD_TYPE)
    

endif(NOT AADC_BUILD_ALL_IN_ONE)

#-------General------------

set(AADC_FOUND FALSE)
set(AADC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../)
find_package(AADC REQUIRED)
if (AADC_FOUND)
   message("-- AADC found")
else(AADC_FOUND)
   message(FATAL_ERROR "-- AADC not found")
endif (AADC_FOUND)

find_package(ADTF 3.3.0 REQUIRED)
message(STATUS "Found ADTF: ${ADTF_VERSION}")

#--------------add private macros-----------------
include(${AADC_DIR}/AADC_PRIVATE.cmake)
include(${AADC_DIR}/AADCConfigVersion.cmake)

#--------------sources----------------------------
include_directories(${AADC_DIR}/include)
include_directories(${CMAKE_INSTALL_INCLUDE})


# ------ included directories ------
add_subdirectory(OpenCVTemplate)
add_subdirectory(TemplateFilter)

add_subdirectory(Sensors)
add_subdirectory(Actuators)

#include_directories(Helpers)
#add_subdirectory(Helpers)
#target_link_libraries(${PROJECT_NAME} HELPERS)
add_subdirectory(EmergencyBrake)
add_subdirectory(LaneDetection)
add_subdirectory(BirdsEyeTransform)
add_subdirectory(ObjectDetection)

add_subdirectory(EnvironmentModel)
add_subdirectory(GoalControl)
add_subdirectory(MissionControl)

add_subdirectory(OpenDriveAnalyzer)

