cmake_minimum_required(VERSION 3.17)
project(BGAL VERSION 1.0)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)

# Default to Release build if not specified
if(NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type selected, defaulting to Release")
    set(CMAKE_BUILD_TYPE Release)
endif()

# Set lib output directories (for archive targets)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)

# Set installation prefix option
option(CMAKE_INSTALL_PREFIX "BGAL install PATH" "/usr/local")

# Add additional CMake modules if needed
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

# libigl
include(libigl)

# Include project headers
include_directories(${PROJECT_SOURCE_DIR}/include)

# Find required packages

# Eigen3
find_package(Eigen3 REQUIRED)
if(Eigen3_FOUND)
    message(STATUS "Eigen3 ${EIGEN3_VERSION_STRING} found")
endif()

# Boost
find_package(Boost REQUIRED)
if(Boost_FOUND)
    message(STATUS "Boost found")
    include_directories(${Boost_INCLUDE_DIRS})
endif()

# CGAL
find_package(CGAL REQUIRED)
if(CGAL_FOUND)
    message(STATUS "CGAL found")
else()
    message(FATAL_ERROR "ERROR: CGAL is required and was not found!")
endif()

# Windows-specific postfix settings
if(WIN32 AND NOT MINGW)
    if(NOT DEFINED CMAKE_DEBUG_POSTFIX)
        set(CMAKE_DEBUG_POSTFIX "d")
    endif()
    if(NOT DEFINED CMAKE_RELWITHDEBINFO_POSTFIX)
        set(CMAKE_RELWITHDEBINFO_POSTFIX "rd")
    endif()
    if(NOT DEFINED CMAKE_MINSIZEREL_POSTFIX)
        set(CMAKE_MINSIZEREL_POSTFIX "s")
    endif()
endif()

# Add subdirectories for project components
add_subdirectory(include)
add_subdirectory(src)
add_subdirectory(MAIN)

# Installation rules for targets and headers
install(TARGETS Algorithm BaseShape Draw Geodesic Integral Model Optimization PointCloudProcessing PQP Reconstruction Tessellation2D Tessellation3D CVTLike
    EXPORT BGALTargets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    PUBLIC_HEADER DESTINATION include
)

install(DIRECTORY ./include/ DESTINATION include
    FILES_MATCHING PATTERN "*.h"
)

configure_file(${PROJECT_NAME}-config.cmake.in ${PROJECT_NAME}-config.cmake @ONLY)
install(EXPORT BGALTargets
    FILE ${PROJECT_NAME}-config.cmake
    NAMESPACE ${PROJECT_NAME}::
    DESTINATION lib/cmake/${PROJECT_NAME}
)
