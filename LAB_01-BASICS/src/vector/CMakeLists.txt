cmake_minimum_required(VERSION 3.0)

project(bench)

add_executable(bench main.c vector.c compute.c)
target_include_directories(bench PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_compile_options(bench PUBLIC -Wall -Wextra)




if(CMAKE_C_COMPILER_ID STREQUAL "GNU")
	set(DEBUG_OPTIONS -O0 -g3)
	set(RELEASE_OPTIONS -O2 -g)
	set(OPTIMIZED_OPTIONS -Ofast -march=native -mtune=native -mavx2 -finline-functions -funroll-loops -fpeel-loops -ftree-vectorize -ftree-loop-vectorize)
elseif(CMAKE_C_COMPILER_ID STREQUAL "Clang")
        set(DEBUG_OPTIONS -O0 -g3)
        set(RELEASE_OPTIONS -O2 -g)
        set(OPTIMIZED_OPTIONS -Ofast)	
else()
        set(DEBUG_OPTIONS -O0 -g3)
        set(RELEASE_OPTIONS -O2 -g)
        set(OPTIMIZED_OPTIONS -Ofast)
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Optimized")
	target_compile_options(bench PUBLIC ${OPTIMIZED_OPTIONS})
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
	target_compile_options(bench PUBLIC ${RELEASE_OPTIONS})
elseif(CMAKE_BUILD_TYPE STREQUAL "Debug")
	target_compile_options(bench PUBLIC ${DEBUG_OPTIONS})
else()
	message(WARNING "Build type not supported: ${BUILD_TYPE}. Please try Debug, Release or Optimized.")
	set(CMAKE_DEBUG_VERSION Release)
endif()

