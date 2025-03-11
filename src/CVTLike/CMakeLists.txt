cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_CVTLike_SRC
    CPD.cpp
    CVT.cpp
)

# Find OpenMP
find_package(OpenMP REQUIRED)

# Create the static library for CVTLike
add_library(CVTLike STATIC ${BGAL_CVTLike_SRC})

# Set multiple properties for the CVTLike target in one call
set_target_properties(CVTLike PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Add definitions
add_definitions(-DNOMINMAX)

# Include directories
target_include_directories(CVTLike PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(CVTLike 
    Algorithm 
    BaseShape 
    Model 
    Tessellation2D 
    Tessellation3D 
    Optimization 
    OpenMP::OpenMP_CXX 
    CGAL::CGAL 
    ${Boost_LIBRARIES}
    igl::core
)
