cmake_minimum_required(VERSION 3.14)
project(OpenGLTutorial)

set(GLFW_SOURCE_DIR "external/glfw")
set(GLEW_SOURCE_DIR "external/glew")
set(GLM_SOURCE_DIR "external/glm")

# Building only the GLFW lib
set(BUILD_SHARED_LIBS OFF CACHE BOOL "")
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "")
set(GLFW_BUILD_TESTS OFF CACHE BOOL "")
set(GLFW_BUILD_DOCS OFF CACHE BOOL "")
set(GLFW_INSTALL OFF CACHE BOOL "")

add_subdirectory(${GLFW_SOURCE_DIR} ${GLEW_SOURCE_DIR})

include_directories(${GLFW_SOURCE_DIR}/include
        ${GLFW_SOURCE_DIR}/deps
        ${GLM_SOURCE_DIR}
        ${GLEW_SOURCE_DIR}/include
        )

add_library(glew STATIC
        ${GLEW_SOURCE_DIR}/src/glew.c
        ${GLEW_SOURCE_DIR}/include
        )

target_link_libraries(glew ${GLFW_LIBRARIES})

add_definitions(
        -DGLEW_STATIC
)

#set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_CXX_STANDARD 17)

# OpenGL
find_package(OpenGL REQUIRED)
include_directories(${OpenGL_INCLUDE_DIRS})
link_directories(${OpenGL_LIBRARY_DIRS})
add_definitions(${OpenGL_DEFINITIONS})

add_executable(OpenGLTutorial main.cpp)
target_link_libraries(OpenGLTutorial glfw ${GLFW_LIBRARIES} glew ${OPENGL_LIBRARIES})


# GLFW
#set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
#set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
#set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
#add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../external/glfw-3.3 glfw-build)
#include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../external/glfw-3.3/include)

# GLEW
#set(CMAKE_PREFIX_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../external/glew-2.1.0")
#set(CMAKE_LIBRARY_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../external/glew-2.1.0/lib/Release/Win32/")
#add_library(glew32s STATIC IMPORTED)
#set_property(TARGET glew32s PROPERTY IMPORTED_LOCATION ${PROJECT_SOURCE_DIR}/deps/glew32s.lib)
#include_directories(deps/glew-2.1.0/include)

#find_package(GLEW REQUIRED)
#target_link_libraries(YourTarget GLEW::GLEW)
#find_path(GLEW_INCLUDE_DIR GL/glew.h)
#find_library(GLEW_LIBRARY NAMES GLEW glew32 glew glew32s PATH_SUFFIXES lib64)

#add_subdirectory(deps/glew-2.1.0/)
#link_directories(deps/glew-2.1.0/lib)
#add_definitions(-DGLEW_STATIC)
#link_libraries(../external/glew-2.1.0/libs)
