# Specify the minimum version of CMake required
cmake_minimum_required(VERSION 3.0)

# Set the project name and language
project(run_servo C)

# Add an executable target called run_servo
add_executable(run_servo PCA9685.c main.c)

# Specify include directories
target_include_directories(run_servo PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

# Optionally, set compiler flags
# target_compile_options(run_servo PRIVATE -Wall -Wextra)

# Define a target for cleaning up build artifacts
add_custom_target(clean
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/cmake_clean.cmake
)

# Generate cmake_clean.cmake to clean up build artifacts
file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/cmake_clean.cmake
    "file(REMOVE_RECURSE ${CMAKE_CURRENT_BINARY_DIR}/CMakeFiles)\n"
    "file(REMOVE_RECURSE ${CMAKE_CURRENT_BINARY_DIR}/run_servo)\n"
    "file(REMOVE ${CMAKE_CURRENT_BINARY_DIR}/CMakeCache.txt)\n"
    "file(REMOVE ${CMAKE_CURRENT_BINARY_DIR}/cmake_install.cmake)\n"
    "file(REMOVE ${CMAKE_CURRENT_BINARY_DIR}/Makefile)\n"
)
