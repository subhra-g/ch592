cmake_minimum_required(VERSION 3.23)

project("ch590x" # VERSION ??.??.??
		DESCRIPTION "CH592HAL"
		HOMEPAGE_URL "https://github.com/openwch/ch592/tree/main/EVT/EXAM"
		LANGUAGES C CXX ASM)

if(NOT DEFINED MCU)
	message(FATAL_ERROR "MCU not defined to build CH32V20x HAL")
endif()

#if(NOT TARGET ch59x_config)
#	message(FATAL_ERROR "ch59x_config target is required. This target should have include path which holds ch32v20x_conf.h and system_ch32v20x.h.")
#endif()

# ToDo: Following way of setting MCU specific option doesn't make sense when it is consumed using FetchContent.
#       But it is required when built as package (to be consumed by  find_package).
#       How to satisfy both use case?
#include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/${MCU}.cmake)

# This is the manufacturer provided HAL.
#option(HAL_USE_DEBUG "" OFF)
set(sdk_path "${CMAKE_CURRENT_SOURCE_DIR}/SRC")
add_subdirectory(SRC)

#if(USE_INSTALL_WIP)
#include(cmake/install.cmake)
#endif()
