project(NorMIT)
cmake_minimum_required(VERSION 2.8.12.2)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_INCLUDE_CURRENT_DIR_IN_INTERFACE ON)

set(NorMIT_VERSION 0.0.1)

include(GenerateExportHeader)

add_library(NorMIT SHARED 
    nmExampleClass.cpp
    nmExampleClass.h
    )
    
generate_export_header(NorMIT)

set (NorMIT_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})
set (NorMIT_LIBRARY_DIRS ${CMAKE_CURRENT_BINARY_DIR})
#set (NorMIT_LIBRARIES "@NorMIT_LIBRARY@")

target_include_directories(NorMIT
    PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_BINARY_DIR}
)


configure_file (
    "${PROJECT_SOURCE_DIR}/cmake/NorMITConfig.cmake.in"
    "${PROJECT_BINARY_DIR}/NorMITConfig.cmake"
    )