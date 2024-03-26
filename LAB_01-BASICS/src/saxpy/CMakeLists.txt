cmake_minimum_required(VERSION 3.0)

project(mainn)

add_executable(base     main.c)
add_executable(modified main_modified.c)

target_include_directories(base     PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(modified PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})


target_compile_options(base     PUBLIC -Wall -Wextra -fdump-tree-all)
target_compile_options(modified PUBLIC -Wall -Wextra)


set(DEBUG_OPTIONS -O0 -g3)
set(RELEASE_OPTIONS -O1 -g)
set(OPTIMIZED_OPTIONS -Ofast)



if(CMAKE_BUILD_TYPE STREQUAL "Optimized")
	target_compile_options(base     PUBLIC ${OPTIMIZED_OPTIONS})
        target_compile_options(modified PUBLIC ${OPTIMIZED_OPTIONS})
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
	target_compile_options(base     PUBLIC ${RELEASE_OPTIONS})
        target_compile_options(modified PUBLIC ${RELEASE_OPTIONS})

elseif(CMAKE_BUILD_TYPE STREQUAL "Debug")
	target_compile_options(base     PUBLIC ${DEBUG_OPTIONS})
        target_compile_options(modified PUBLIC ${DEBUG_OPTIONS})
	
else()
	message(WARNING "Build type not supported: ${BUILD_TYPE}. Please try Debug, Release or Optimized.")
	set(CMAKE_DEBUG_VERSION Release)
endif()





