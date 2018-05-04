cmake_minimum_required(VERSION 2.6)

project(gpr)

#set(CMAKE_CXX_FLAGS_DEBUG "-g")
#set(CMAKE_CXX_FLAGS_RELEASE "-O2")

#SET(EXTRA_CXX_COMPILE_FLAGS "-std=c++11 -I./src -I./test -Werror -Wall")
#SET(EXTRA_CXX_COMPILE_FLAGS "-std=c++11 -I./src -I./test -Wall")

SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} ${EXTRA_CXX_COMPILE_FLAGS}")

OPTION(GPR_BUILD_TESTS "Build gpr tests" ON)
option(GPR_BUILD_SAMPLE "Build gpr sample" ON)

INCLUDE_DIRECTORIES(./src/)

SET(GPR_HEADERS src/gcode_program.h
		src/parser.h)

SET(GPR_CPPS src/parser.cpp
	     src/gcode_program.cpp)

add_library(gpr ${GPR_CPPS} ${GPR_HEADERS})

SET(TEST_FILES test/parser_tests.cpp
	       test/main.cpp)

IF(GPR_BUILD_TESTS)
	add_executable(all-tests ${TEST_FILES})
	target_link_libraries(all-tests gpr)
ENDIF(GPR_BUILD_TESTS)

IF(GPR_BUILD_SAMPLE)
	add_executable(parse-gcode src/main.cpp)
	target_link_libraries(parse-gcode gpr)
ENDIF(GPR_BUILD_SAMPLE)
