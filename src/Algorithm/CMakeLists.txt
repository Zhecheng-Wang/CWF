cmake_minimum_required(VERSION 3.17)

# Optionally define VERSION if not already set
set(VERSION 1.0)

set(BGAL_Algorithm_SRC        
        BOC/BOC.cpp
)

# Create the static library for Algorithm
add_library(Algorithm STATIC ${BGAL_Algorithm_SRC})

# Set multiple properties for the Algorithm target in one call
set_target_properties(Algorithm PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

target_include_directories(Algorithm PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)