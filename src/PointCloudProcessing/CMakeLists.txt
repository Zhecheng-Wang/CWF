cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_PointCloudProcessing_SRC        
    Registration/ICP/ICP.cpp
)

# Create the static library for PointCloudProcessing
add_library(PointCloudProcessing STATIC ${BGAL_PointCloudProcessing_SRC})

# Set multiple properties for the PointCloudProcessing target in one call
set_target_properties(PointCloudProcessing PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(PointCloudProcessing PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(PointCloudProcessing 
    Algorithm 
    BaseShape 
    ${Boost_LIBRARIES}
)
