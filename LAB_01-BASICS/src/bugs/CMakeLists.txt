cmake_minimum_required(VERSION 3.0)

project(bugs)

add_executable(bugs main.c)
add_executable(correct main_modified.c)

target_include_directories(bugs PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(correct PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})


target_compile_options(bugs PUBLIC -Wall -Wextra)
target_compile_options(correct PUBLIC -Wall -Wextra)



if(CMAKE_C_COMPILER_ID STREQUAL "GNU")
	set(DEBUG_OPTIONS -O0 -g3)
	set(RELEASE_OPTIONS -O2 -g)
	set(OPTIMIZED_OPTIONS -Ofast -march=native -mtune=native -mavx2 -finline-functions -funroll-loops -fpeel-loops -ftree-vectorize -ftree-loop-vectorize)
elseif(CMAKE_C_COMPILER_ID STREQUAL "Clang")
        set(DEBUG_OPTIONS -O0 -g3)
        set(RELEASE_OPTIONS -O2 -g)
        set(OPTIMIZED_OPTIONS -Ofast -march=native -mtune=native -mavx2 -finline-functions -funroll-loops -fpeel-loops -Rpass-analysis=loop-vectorize -Rpass=loop-vectorize)	
else()
        set(DEBUG_OPTIONS -O0 -g3)
        set(RELEASE_OPTIONS -O2 -g3)
        set(OPTIMIZED_OPTIONS -Ofast -g3)
endif()



if(CMAKE_BUILD_TYPE STREQUAL "Optimized")
	target_compile_options(bugs PUBLIC ${OPTIMIZED_OPTIONS})
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
	target_compile_options(bugs PUBLIC ${RELEASE_OPTIONS})
elseif(CMAKE_BUILD_TYPE STREQUAL "Debug")
	target_compile_options(bugs PUBLIC ${DEBUG_OPTIONS})
else()
	message(WARNING "Build type not supported: ${BUILD_TYPE}. Please try Debug, Release or Optimized.")
	set(CMAKE_DEBUG_VERSION Release)
endif()





