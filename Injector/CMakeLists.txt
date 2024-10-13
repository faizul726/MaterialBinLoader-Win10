cmake_minimum_required(VERSION 3.21)

project(Injector)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Specify the executable
add_executable(Injector main.cpp)

# Link with the MaterialBinLoader library
target_link_libraries(Injector PRIVATE MaterialBinLoader)

# Set output directory for the executable
set_target_properties(Injector PROPERTIES
    OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/Release"
)
