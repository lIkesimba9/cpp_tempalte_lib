project(test_template_lib)
cmake_minimum_required(VERSION 3.16.0)
set(CMAKE_CXX_STANDARD 17) 

IF(APPLE)
    set(CMAKE_THREAD_LIBS_INIT "-lpthread")
    set(CMAKE_HAVE_THREADS_LIBRARY 1)
ENDIF()

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-fsanitize=address -g -fno-omit-frame-pointer -fno-optimize-sibling-calls -fprofile-arcs -ftest-coverage -fPIC -O0 -Wno-pedantic")
IF(APPLE)
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -coverage")
ELSE()
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -coverage -lgcov")
ENDIF()


set(SOURCE_TEST  test.cpp)

find_package(GTest REQUIRED)


add_executable(${PROJECT_NAME} ${SOURCE_TEST})

target_include_directories(${PROJECT_NAME} PUBLIC ${TEMPLATE_LIB_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} LINK_PUBLIC GTest::Main ${TEMPLATE_LIB_LIBRARIES})
set_target_properties(${PROJECT_NAME} PROPERTIES LINKER_LANGUAGE CXX)
