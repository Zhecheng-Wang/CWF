cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_BaseShape_SRC
    KDTree.cpp
    Line.cpp
    Point.cpp
    Polygon.cpp
    Triangle.cpp
)

# Create the static library for BaseShape
add_library(BaseShape STATIC ${BGAL_BaseShape_SRC})

# Set multiple properties for the BaseShape target in one call
set_target_properties(BaseShape PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(BaseShape PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(BaseShape 
    Algorithm 
    ${Boost_LIBRARIES}
    CGAL::CGAL 
    Eigen3::Eigen
)
