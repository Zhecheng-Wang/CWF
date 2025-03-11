cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_Reconstruction_SRC        
    MarchingTerahedra/MarchingTetrahedra.cpp
)

# Create the static library for Reconstruction
add_library(Reconstruction STATIC ${BGAL_Reconstruction_SRC})

# Set multiple properties for the Reconstruction target in one call
set_target_properties(Reconstruction PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(Reconstruction PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(Reconstruction 
    Algorithm 
    BaseShape 
    Model 
    PQP 
    ${Boost_LIBRARIES}
)
