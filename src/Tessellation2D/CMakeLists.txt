cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_Tessellation2D_SRC        
    Side2D.cpp
    Tessellation2D.cpp
)

# Create the static library for Tessellation2D
add_library(Tessellation2D STATIC ${BGAL_Tessellation2D_SRC})

# Set multiple properties for the Tessellation2D target in one call
set_target_properties(Tessellation2D PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(Tessellation2D PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(Tessellation2D 
    Algorithm 
    BaseShape 
    ${Boost_LIBRARIES}
)
