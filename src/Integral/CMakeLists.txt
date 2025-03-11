cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_Integral_SRC        
    Integral.cpp
    Tetrahedron_arbq_rule.cpp
)

# Create the static library for Integral
add_library(Integral STATIC ${BGAL_Integral_SRC})

# Set multiple properties for the Integral target in one call
set_target_properties(Integral PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(Integral PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(Integral 
    Algorithm 
    BaseShape 
    ${Boost_LIBRARIES}
)
