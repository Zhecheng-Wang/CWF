cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_Draw_SRC        
    DrawPS.cpp
)

# Create the static library for Draw
add_library(Draw STATIC ${BGAL_Draw_SRC})

# Set multiple properties for the Draw target in one call
set_target_properties(Draw PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(Draw PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(Draw 
    Algorithm 
    BaseShape 
    ${Boost_LIBRARIES}
)
