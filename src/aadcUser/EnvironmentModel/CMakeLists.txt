cmake_minimum_required(VERSION 3.10.0)

project(environmental_model)

include_directories(${OpenCV_INCLUDE_DIRS})


aux_source_directory(../Helpers HELPERS)
aux_source_directory(./Models MODELS)
aux_source_directory(../Helpers/OpenDriveAnalyzer ODAnalyzer)
aux_source_directory(../Helpers/OpenDriveAnalyzer/mapReader ODMapReader)

set (SOURCEFILES
		stdafx.h

        ${HELPERS}
        ${MODELS}

        ${ODAnalyzer}
        ${ODMapReader}

		EnvironmentalModel.h
		EnvironmentalModel.cpp
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
