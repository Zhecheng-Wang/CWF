cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_PQP_SRC        
    Build.cpp
    BV.cpp
    PQP.cpp
    TriDist.cpp
)

# Create the static library for PQP
add_library(PQP STATIC ${BGAL_PQP_SRC})

# Set multiple properties for the PQP target in one call
set_target_properties(PQP PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(PQP PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)
