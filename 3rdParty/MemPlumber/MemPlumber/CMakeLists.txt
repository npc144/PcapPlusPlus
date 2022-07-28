cmake_minimum_required (VERSION 3.0)
project (memplumber CXX)

add_library (memplumber
	memplumber.cpp
	memplumber.h
)

# Build options
option(COLLECT_STATIC_VAR_DATA	"Collect data also on static variable memory allocation" OFF)
option(BUILD_TESTS  "Build tests" OFF)
option(BUILD_EXAMPLES  "Build examples" OFF)

if(COLLECT_STATIC_VAR_DATA)
    add_definitions(-DCOLLECT_STATIC_VAR_DATA)
endif()

target_include_directories(memplumber PUBLIC
	${CMAKE_CURRENT_SOURCE_DIR}
)

if(BUILD_TESTS)
	enable_testing()
	add_subdirectory(Tests)
endif()

if(BUILD_EXAMPLES)
	add_subdirectory(Examples)
endif()
