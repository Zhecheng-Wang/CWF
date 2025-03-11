cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_Model_SRC        
    Model.cpp
    ManifoldModel.cpp
    Model_Iterator.cpp
)

# Create the static library for Model
add_library(Model STATIC ${BGAL_Model_SRC})

# Set multiple properties for the Model target in one call
set_target_properties(Model PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(Model PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(Model 
    Algorithm 
    BaseShape 
    PQP 
    ${Boost_LIBRARIES}
)
