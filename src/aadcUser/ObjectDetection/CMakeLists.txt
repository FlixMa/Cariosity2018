cmake_minimum_required(VERSION 3.10.0)

project(object_detection_filter_yolos)

aux_source_directory(../Helpers HELPERS)
aux_source_directory(../EnvironmentModel/Models ENVIRONMETAL_MODELS)

include_directories(${OpenCV_INCLUDE_DIRS})

set (SOURCEFILES
        stdafx.h
        ObjectDetectionFilter.cpp
        ObjectDetectionFilter.h
        ${HELPERS}
        ${ENVIRONMETAL_MODELS}
        )


adtf_add_filter(${PROJECT_NAME}
        ${SOURCEFILES})

# Specify where it should be installed to
adtf_install_target(${PROJECT_NAME} bin)

adtf_create_plugindescription(
        TARGET
        ${PROJECT_NAME}
        PLUGIN_SUBDIR
        "bin")

target_link_libraries(${PROJECT_NAME} LINK_PUBLIC ${OpenCV_LIBS})
#target_link_libraries(${PROJECT_NAME} LINK_PUBLIC /usr/lib/libYOLOv3SE.so)

#this is to add a folder within the ADTF solution
set_property(TARGET ${PROJECT_NAME} PROPERTY FOLDER algorithms)
set_property(TARGET ${PROJECT_NAME}_pdgen PROPERTY FOLDER algorithms)
