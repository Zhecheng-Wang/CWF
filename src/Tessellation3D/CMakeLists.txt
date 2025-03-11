cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_Tessellation3D_SRC        
    Side3D.cpp
    Tessellation3D.cpp
)

# Create the static library for Tessellation3D
add_library(Tessellation3D STATIC ${BGAL_Tessellation3D_SRC})

# Set multiple properties for the Tessellation3D target in one call
set_target_properties(Tessellation3D PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(Tessellation3D PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(Tessellation3D 
    Algorithm 
    BaseShape 
    Model 
    ${Boost_LIBRARIES}
)
