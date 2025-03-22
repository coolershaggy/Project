# Set the minimum required version of CMake to 3.10
cmake_minimum_required(VERSION 3.10)

# Define the project name as MyProjects
project(MyProjects)

# Define the available configurations
set(CMAKE_CONFIGURATION_TYPES "Debug;Release;ReleaseInternal" CACHE STRING "" FORCE)

# Set linker flags for ReleaseInternal configuration
# Here we are using same flags as that of RELEASE configuration in ReleaseInternal
set(CMAKE_C_FLAGS_RELEASEINTERNAL "") # or we can set this to empty as well
set(CMAKE_CXX_FLAGS_RELEASEINTERNAL "")
set(CMAKE_EXE_LINKER_FLAGS_RELEASEINTERNAL "${CMAKE_EXE_LINKER_FLAGS_RELEASE}")
set(CMAKE_SHARED_LINKER_FLAGS_RELEASEINTERNAL "${CMAKE_SHARED_LINKER_FLAGS_RELEASE}")

# Global variables for build target and output directories
# BLDTARGET sets the build configuration (Debug, Release, ReleaseInternal)
set(BLDTARGET "$<$<CONFIG:Debug>:Debug>$<$<CONFIG:Release>:Release>$<$<CONFIG:ReleaseInternal>:ReleaseInternal>")

# DSTDIR sets the directory for executable binaries
set(DSTDIR "${CMAKE_BINARY_DIR}/${BLDTARGET}/bin")

# LIBDIR sets the directory for library binaries
set(LIBDIR "${CMAKE_BINARY_DIR}/${BLDTARGET}/lib")

# Define an option to enable or disable ProjectC and ProjectD
# The default value is OFF
option(ENABLE_CD "Enable project C and D" OFF)

# Conditionally add subdirectories for ProjectC and ProjectD
# if the ENABLE_CD option is set to ON
if(ENABLE_CD)
    add_subdirectory(ProjectC)
    add_subdirectory(ProjectD)
endif()

# Always add subdirectories for ProjectA and ProjectB
add_subdirectory(ProjectA)
add_subdirectory(ProjectB)