# Set the minimum required version of CMake to 3.10
cmake_minimum_required(VERSION 3.10)

# Define the project name as ProjectD
project(ProjectD)

# Include the directory where utils.h from ProjectB is located
include_directories(${CMAKE_SOURCE_DIR}/ProjectB)

# Add an executable target named ProjectD from the source file main.cpp
add_executable(ProjectD main.cpp)

# Link the ProjectD executable with the ProjectB library
target_link_libraries(ProjectD ProjectB)

# Set output directories for the ProjectA executable
set_target_properties(ProjectD PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${DSTDIR}
    RUNTIME_OUTPUT_DIRECTORY_DEBUG ${DSTDIR}
    RUNTIME_OUTPUT_DIRECTORY_RELEASE ${DSTDIR}
    RUNTIME_OUTPUT_DIRECTORY_RELEASEINTERNAL ${DSTDIR}
    LIBRARY_OUTPUT_DIRECTORY ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_DEBUG ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_RELEASE ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_RELEASEINTERNAL ${LIBDIR}
)