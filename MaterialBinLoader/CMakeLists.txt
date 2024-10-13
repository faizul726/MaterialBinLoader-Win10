cmake_minimum_required(VERSION 3.21)

project(MaterialBinLoader)

# Set C++ standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Set build type to Release by default
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

# Collect source files
file(GLOB_RECURSE SRC_FILES_DIR
    "${PROJECT_SOURCE_DIR}/*.c"
    "${PROJECT_SOURCE_DIR}/*.cpp"
    "${PROJECT_SOURCE_DIR}/*.h"
    "${PROJECT_SOURCE_DIR}/Hook/*.c"
    "${PROJECT_SOURCE_DIR}/Hook/*.cpp"
    "${PROJECT_SOURCE_DIR}/Hook/*.h"
)

# Include directories
include_directories(
    "${CMAKE_SOURCE_DIR}/include"
)

# Link directories
link_directories(
    "${CMAKE_SOURCE_DIR}/lib"
)

# Add compile definitions
add_definitions(
    -D"NDEBUG"
    -D"NOMINMAX"
    -D"TEMPLATE_EXPORTS"
    -D"UNICODE"
    -D"WIN32_LEAN_AND_MEAN"
    -D"_AMD64_"
    -D"_CRT_SECURE_NO_WARNINGS"
    -D"_UNICODE"
    -D"_USRDLL"
    -D"_WINDLL"
    -D"_WINDOWS"
)

# Add compile options
add_compile_options(
    /diagnostics:column
    /EHsc
    /FC
    /GL
    /MD
    /nologo
    /permissive-
    /sdl
    /utf-8
    /Zc:inline
    /Zi
)

# Add link options
add_link_options(
    /DEBUG
    /DLL
    /IGNORE:4199
    /INCREMENTAL:NO
    /LTCG
    /MANIFESTUAC:NO
    /MACHINE:X64
    /NOLOGO
    /OPT:ICF
    /OPT:REF
    /SUBSYSTEM:CONSOLE
)

# Create shared library
add_library(MaterialBinLoader SHARED ${SRC_FILES_DIR})

# Link with Detours library
target_link_libraries(MaterialBinLoader
    "${CMAKE_SOURCE_DIR}/lib/detours.lib"
)

# Specify output directory for the DLL
set_target_properties(MaterialBinLoader PROPERTIES
    OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/Release"
)
