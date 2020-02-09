# CMake entry point.
# Note that this CMakeLists.txt in fully independent from the one in the parent directory
# (since that's the goal of this tutorial !)

# For an introduction to CMake, see
# http://www.cmake.org/cmake/help/cmake_tutorial.html (at least steps 1 and 2)

cmake_minimum_required (VERSION 2.6)
project (Sample2)

# Use the C++11 standard.
set(CMAKE_CXX_FLAGS "-std=c++11")
# Suppress warnings of the deprecation of glut functions on macOS.
if(APPLE)
 add_definitions(-Wno-deprecated-declarations)
endif()

find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)

if(UNIX AND NOT APPLE)
 find_package(GLEW REQUIRED)
endif()

set(INCLUDE_DIRS ${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIR})
set(LIBRARIES ${OPENGL_LIBRARIES} ${GLUT_LIBRARIES})

if(UNIX AND NOT APPLE)
 list(APPEND INCLUDE_DIRS ${GLEW_INCLUDE_DIRS})
 list(APPEND LIBRARIES ${GLEW_LIBRARIES})
endif()

include_directories(${INCLUDE_DIRS})

file(GLOB SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.cc)
file(GLOB INCLUDE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.h)


# triangle project
add_executable(triangle ${SOURCE_FILES} ${INCLUDE_FILES})

target_link_libraries(triangle ${LIBRARIES})
