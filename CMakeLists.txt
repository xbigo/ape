cmake_minimum_required(VERSION 3.14)

project(Ape
	VERSION "0.1.0"
	DESCRIPTION "A collection of small C++ libraries"
	LANGUAGES CXX)

set(APE_SUPERPROJECT Ape)
set(APE_SUPERPROJECT_VERSION ${PROJECT_VERSION})
set(APE_SUPERPROJECT_SOURCE_DIR ${PROJECT_SOURCE_DIR})
list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/libs/amun/lib/amun)

if (AMUN_INCLUDED)
	message(WARNING "Ape expects to use amun from itself")
else()
	include(${CMAKE_CURRENT_SOURCE_DIR}/libs/amun/lib/amun/amun.cmake)
	if (NOT AMUN_INCLUDED)
		message(FATAL_ERROR "Failed to include Amun")
	endif()
endif()
amun_disable_build_in_source()

if (BUILD_TESTING)
	set(APE_BUILD_TESTING ${BUILD_TESTING})
endif()

amun_check_build(CONFIG NORMAL INSTALL TEST)

if(${CONFIG_INSTALL})
	add_library(Ape INTERFACE)
	amun_get_cmake_install_dir(APE_INSTALL_DIR)

	#TODO: write config.cmake
	amun_install_targets(${APE_INSTALL_DIR} Ape)
	amun_install_config_version(${APE_INSTALL_DIR})

	install(FILES cmake/ApeConfig-include.cmake DESTINATION ${APE_INSTALL_DIR})
endif()

if(${CONFIG_TEST})
	amun_enable_testing()
endif()

add_subdirectory(libs/amun)
add_subdirectory(libs/config)
add_subdirectory(libs/estl)
