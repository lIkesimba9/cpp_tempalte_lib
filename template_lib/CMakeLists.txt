project(template_lib)
cmake_minimum_required(VERSION 3.16.0)
set(CMAKE_CXX_STANDARD 17) 
set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-fsanitize=address -g -fno-omit-frame-pointer -fno-optimize-sibling-calls -fprofile-arcs -ftest-coverage -fPIC -O0 -Wall -Werror -Wpedantic -Wno-unused-variable")


file(GLOB SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)
file(GLOB INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/include)


add_library(${PROJECT_NAME} ${SOURCES} )

target_include_directories(${PROJECT_NAME} PUBLIC ${INCLUDE_DIRS})

set(TEMPLATE_LIB_LIBRARIES ${PROJECT_NAME} PARENT_SCOPE)
set(TEMPLATE_LIB_INCLUDE_DIRS ${INCLUDE_DIRS} PARENT_SCOPE)

