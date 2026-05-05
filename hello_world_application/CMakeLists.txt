cmake_minimum_required(VERSION 3.5)
project(hello_world)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_CXX_STANDARD_REQUIRED ON)


add_executable(hello_world ${CMAKE_CURRENT_SOURCE_DIR}/hello_world.cpp)

target_include_directories(hello_world PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
)
target_link_libraries(hello_world PRIVATE formatter_ex)
