cmake_minimum_required(VERSION 3.0)

project(bench)

add_executable(bench main.c vector.c compute.c)
target_include_directories(bench PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

