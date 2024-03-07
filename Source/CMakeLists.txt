cmake_minimum_required(VERSION 3.18) # Recommended version for better CUDA integration
project(time_measurement CUDA CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CUDA_STANDARD 11)

# Optimization
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -fopenmp")
set(CMAKE_CUDA_FLAGS "${CMAKE_CUDA_FLAGS} -O3")

# Find CUDA Toolkit
find_package(CUDA REQUIRED)
include_directories(${CUDA_INCLUDE_DIRS})

# Find GDAL
find_package(GDAL REQUIRED)
if(GDAL_FOUND)
    include_directories(${GDAL_INCLUDE_DIRS})
endif()

# Collect all CPP and CU source files
file(GLOB PROJECT_SOURCES "*.cpp")
file(GLOB PROJECT_CUDA_SOURCES "*.cu")

# Create executable
add_executable(time_measurement ${PROJECT_SOURCES} ${PROJECT_CUDA_SOURCES})

# Link libraries
target_link_libraries(time_measurement ${GDAL_LIBRARIES} ${CUDA_LIBRARIES})
