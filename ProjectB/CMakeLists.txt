# Set the minimum required version of CMake to 3.10
cmake_minimum_required(VERSION 3.10)

# Define the project name as ProjectB
project(ProjectB)

# Add a static library target named ProjectB from the source file utils.cpp
add_library(ProjectB utils.cpp)

# Set output directories for the ProjectB library
set_target_properties(ProjectB PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_DEBUG ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_RELEASE ${LIBDIR}
    LIBRARY_OUTPUT_DIRECTORY_RELEASEINTERNAL ${LIBDIR}
    ARCHIVE_OUTPUT_DIRECTORY ${LIBDIR}
    ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${LIBDIR}
    ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${LIBDIR}
    ARCHIVE_OUTPUT_DIRECTORY_RELEASEINTERNAL ${LIBDIR}
)