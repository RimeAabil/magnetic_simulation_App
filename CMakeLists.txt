cmake_minimum_required(VERSION 3.16)
project(crist-project)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find Raylib (with fallback)
find_package(raylib QUIET)
if(NOT raylib_FOUND)
    # If not found in system paths, look in common install locations
    find_path(RAYLIB_INCLUDE_DIR raylib.h
              PATHS /usr/local/include /usr/include)
    find_library(RAYLIB_LIBRARY NAMES raylib
                 PATHS /usr/local/lib /usr/lib)
    
    if(RAYLIB_INCLUDE_DIR AND RAYLIB_LIBRARY)
        add_library(raylib UNKNOWN IMPORTED)
        set_target_properties(raylib PROPERTIES
            IMPORTED_LOCATION "${RAYLIB_LIBRARY}"
            INTERFACE_INCLUDE_DIRECTORIES "${RAYLIB_INCLUDE_DIR}")
        message(STATUS "Found Raylib: ${RAYLIB_LIBRARY}")
    else()
        message(FATAL_ERROR "Raylib not found! Please install it first.")
    endif()
endif()

# Add executable
add_executable(crist-project src/main.cpp)

# Link Raylib and system libraries
target_link_libraries(crist-project raylib)

# Platform-specific libraries
if(UNIX AND NOT APPLE)
    target_link_libraries(crist-project m pthread dl)
endif()

# Set output directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Enable warnings
if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
    target_compile_options(crist-project PRIVATE -Wall -Wextra)
endif()
