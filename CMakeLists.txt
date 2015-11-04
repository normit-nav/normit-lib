project(NorMITLib)
cmake_minimum_required(VERSION 3.0)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_INCLUDE_CURRENT_DIR_IN_INTERFACE ON)

set(NorMIT_VERSION 0.0.1)

include(GenerateExportHeader)

add_library(NorMIT SHARED 
    nmExampleClass.cpp
    nmExampleClass.h
    )
    
generate_export_header(NorMIT)
set_property(TARGET NorMIT PROPERTY VERSION ${NorMIT_VERSION})
set_property(TARGET NorMIT PROPERTY SOVERSION 0)
set_property(TARGET NorMIT PROPERTY
  INTERFACE_NorMIT_MAJOR_VERSION 3)
set_property(TARGET NorMIT APPEND PROPERTY
  COMPATIBLE_INTERFACE_STRING NorMIT_MAJOR_VERSION
)

install(TARGETS NorMIT EXPORT NorMITTargets
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
  INCLUDES DESTINATION include
)
install(
  FILES
    nmExampleClass.h
    "${CMAKE_CURRENT_BINARY_DIR}/NorMIT_export.h"
  DESTINATION
    include
  COMPONENT
    Devel
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/NorMIT/NorMITConfigVersion.cmake"
  VERSION ${NorMIT_VERSION}
  COMPATIBILITY AnyNewerVersion
)

export(EXPORT NorMITTargets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/NorMIT/NorMITTargets.cmake"
  NAMESPACE nm::
)
configure_file(cmake/NorMITConfig.cmake
  "${CMAKE_CURRENT_BINARY_DIR}/NorMIT/NorMITConfig.cmake"
  COPYONLY
)

set(ConfigPackageLocation lib/cmake/NorMIT)
install(EXPORT NorMITTargets
  FILE
    NorMITTargets.cmake
  NAMESPACE
    nm::
  DESTINATION
    ${ConfigPackageLocation}
)
install(
  FILES
    cmake/NorMITConfig.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/NorMIT/NorMITConfigVersion.cmake"
  DESTINATION
    ${ConfigPackageLocation}
  COMPONENT
    Devel
)