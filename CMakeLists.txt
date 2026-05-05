
cmake_minimum_required(VERSION 3.5)
project(solver VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex)
add_subdirectory(solver_lib)

add_subdirectory(hello_world_application)
add_subdirectory(solver_application)

