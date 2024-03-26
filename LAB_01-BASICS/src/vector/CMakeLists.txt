cmake_minimum_required(VERSION 3.0)

project(bench)

add_executable(bench main.c vector.c compute.c)
target_include_directories(bench PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_compile_options(bench PUBLIC -Wall -Wextra)




set(DEBUG_OPTIONS -O0 -g3)
set(RELEASE_OPTIONS -O2)
set(OPTIMIZED_OPTIONS -O3 -march=native -mtune=native -mavx2 -finline-functions -funroll-loops -fpeel-loops -ftree-vectorize -ftree-loop-vectorize)


if(CMAKE_BUILD_TYPE STREQUAL "optimized")
	target_compile_options(bench PUBLIC ${OPTIMIZED_OPTIONS})
elseif(CMAKE_BUILD_TYPE STREQUAL "release")
	target_compile_options(bench PUBLIC ${RELEASE_OPTIONS})
elseif(CMAKE_BUILD_TYPE STREQUAL "debug")
	target_compile_options(bench PUBLIC ${DEBUG_OPTIONS})
else()
	message(FATAL_ERROR "Build type not supported: ${BUILD_TYPE}. Please try "debug", "release" or "optimized".")
	set(CMAKE_BUILD_TYPE Release)
endif()
message("Build type: ${CMAKE_BUILD_TYPE}")

