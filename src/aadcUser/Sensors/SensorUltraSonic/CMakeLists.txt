cmake_minimum_required(VERSION 3.10.0)

project(sensor_ultra_sonic)

include_directories(${OpenCV_INCLUDE_DIRS})

set (SOURCEFILES
        ../../Helpers/ddlStructs.h
        ../../Helpers/StdFilter.h
        ../../Helpers/StdFilter.cpp
        ../../Helpers/stdafx.h
        ../../Helpers/Median.h
        ../../Helpers/Median.cpp

        stdafx.h

        SensorUltraSonic.h
        SensorUltraSonic.cpp
)

adtf_add_filter(${PROJECT_NAME}
				${SOURCEFILES}
)

# Specify where it should be installed to
adtf_install_target(${PROJECT_NAME} bin)

adtf_create_plugindescription(
        TARGET
        ${PROJECT_NAME}
        PLUGIN_SUBDIR
        "bin"
)

target_link_libraries(${PROJECT_NAME} LINK_PUBLIC ${OpenCV_LIBS})

#this is to add a folder within the ADTF solution
set_property(TARGET ${PROJECT_NAME} PROPERTY FOLDER user)
set_property(TARGET ${PROJECT_NAME}_pdgen PROPERTY FOLDER user)
