cmake_minimum_required(VERSION 2.8)

set(PROJECT_NAME "lsl")
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "-O3")

project(${PROJECT_NAME})

add_definitions("-std=c++11")
add_definitions("-Wall -Wextra -pedantic")

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/include")

find_package(Eigen3 3.0 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})

find_package(wxWidgets 3.0 REQUIRED core base)
include(${wxWidgets_USE_FILE})
include_directories(${wxWidgets_INCLUDE_DIRS})
add_definitions(${wxWidgets_CXX_FLAGS})

file(GLOB CPPS "src/lsl/*/*.cpp")
file(GLOB HPPS "include/lsl/*/*.hpp")

add_library(${PROJECT_NAME} SHARED ${CPPS} ${HPPS})

target_link_libraries(${PROJECT_NAME} ${wxWidgets_LIBRARIES})