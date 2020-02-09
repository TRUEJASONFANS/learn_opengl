cmake_minimum_required(VERSION 3.11)
project(OpenGLStudy1)

find_package(OpenGL REQUIRED)
if(APPLE AND NOT IPHONE)
set(MACOSX 1)
endif(APPLE AND NOT IPHONE)

if(MACOSX)
find_library(carbon_lib Carbon)
find_library(iokit_lib IOKit)
find_library(forcefeedback_lib ForceFeedback)
find_library(cocoa_lib Cocoa)
find_library(audiounit_lib AudioUnit)
find_library(corevideo_lib CoreVideo)
find_library(coreaudio_lib CoreAudio)
find_library(opengl_lib OpenGL)
find_library(corefoundation_lib CoreFoundation)
set(frameworks
    ${carbon_lib}
    ${iokit_lib}
    ${forcefeedback_lib}
    ${cocoa_lib}
    ${audiounit_lib}
    ${coreaudio_lib}
    ${corevideo_lib}
    ${opengl_lib}
    ${corefoundation_lib})
endif(MACOSX)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(SOURCES main.cc glad.c)

add_executable(OpenGL ${SOURCES})
target_include_directories(OpenGL PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/dependencies/GLFW)
target_include_directories(OpenGL PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/dependencies)
target_link_libraries(OpenGL ${OPENGL_LIBRARIES} ${CMAKE_CURRENT_SOURCE_DIR}/dependencies/GLFW/lib/libglfw3.a ${frameworks})