# Set the minimum required version of CMake to 3.10
cmake_minimum_required(VERSION 3.10)

# Define the project name as ProjectC
project(ProjectC)

# Include the directory where utils.h from ProjectB is located
include_directories(${CMAKE_SOURCE_DIR}/ProjectB)

# Add an executable target named ProjectC from the source file main.cpp
add_executable(ProjectC main.cpp)

# Link the ProjectC executable with the ProjectB library
target_link_libraries(ProjectC ProjectB)

# Set output directories for the ProjectC executable
set_target_properties(ProjectC PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${DSTDIR}
    RUNTIME_OUTPUT_DIRECTORY_DEBUG ${DSTDIR}
    RUNTIME_OUTPUT_DIRECTORY_RELEASE ${DSTDIR}
    RUNTIME_OUTPUT_DIRECTORY_RELEASEINTERNAL ${DSTDIR}
    LIBRARY_OUTPUT_DIRECTORY ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_DEBUG ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_RELEASE ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_RELEASEINTERNAL ${LIBDIR}
)