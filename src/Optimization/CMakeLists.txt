cmake_minimum_required(VERSION 3.17)

# Ensure VERSION is defined
set(VERSION 1.0)

set(BGAL_Optimization_SRC
    ALGLIB/alglibinternal.cpp
    ALGLIB/alglibmisc.cpp
    ALGLIB/ap.cpp
    ALGLIB/dataanalysis.cpp
    ALGLIB/diffequations.cpp
    ALGLIB/fasttransforms.cpp
    ALGLIB/integration.cpp
    ALGLIB/interpolation.cpp
    ALGLIB/linalg.cpp
    ALGLIB/optimization.cpp
    ALGLIB/solvers.cpp
    ALGLIB/specialfunctions.cpp
    ALGLIB/statistics.cpp
    LBFGS/LBFGS.cpp
    GradientDescent/GradientDescent.cpp
    LinearSystem/LinearSystem.cpp
)

# Create the static library for Optimization
add_library(Optimization STATIC ${BGAL_Optimization_SRC})

# Set multiple properties for the Optimization target in one call
set_target_properties(Optimization PROPERTIES 
    CXX_STANDARD 17
    VERSION ${VERSION}
    CLEAN_DIRECT_OUTPUT 1
)

# Include directories
target_include_directories(Optimization PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Link libraries
target_link_libraries(Optimization 
    Eigen3::Eigen
)
