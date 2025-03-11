cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_Geodesic_SRC        
    Dijkstra/Dijkstra.cpp
    AbstractMethod.cpp
)

# Create the static library for Geodesic
add_library(Geodesic STATIC ${BGAL_Geodesic_SRC})

# Set multiple properties for the Geodesic target in one call
set_target_properties(Geodesic PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(Geodesic PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(Geodesic 
    BaseShape 
    Algorithm 
    Model 
    PQP 
    ${Boost_LIBRARIES}
)
