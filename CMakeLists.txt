cmake_minimum_required(VERSION 2.4.7)
PROJECT(indi-l298n-focuser CXX C)

LIST(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake_modules/")

include(GNUInstallDirs)

set (VERSION_MAJOR 1)
set (VERSION_MINOR 0)

find_package(INDI REQUIRED)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config.h)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/indi_l298n_focuser.xml.cmake ${CMAKE_CURRENT_BINARY_DIR}/indi_l298n_focuser.xml)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${INDI_INCLUDE_DIR})

include(CMakeCommon)

set(GPIO_LIBRARIES "libgpiod.so")

################ L298N Focuser ################
set(indi_l298n_focuser_SRCS
        ${CMAKE_CURRENT_SOURCE_DIR}/l298n_focuser.cpp
   )

IF (UNITY_BUILD)
    ENABLE_UNITY_BUILD(indi_l298n_focuser indi_l298n_focuser_SRCS 6 cpp)
ENDIF ()

add_executable(indi_l298n_focuser ${indi_l298n_focuser_SRCS})
target_link_libraries(indi_l298n_focuser ${INDI_DRIVER_LIBRARIES} ${GPIO_LIBRARIES})
install(TARGETS indi_l298n_focuser RUNTIME DESTINATION bin )
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/indi_l298n_focuser.xml DESTINATION ${INDI_DATA_DIR})
