cmake_minimum_required(VERSION 3.20)

project(OpenGL-Practice LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)

# GLFW
FetchContent_Declare(
    glfw
    GIT_REPOSITORY https://github.com/glfw/glfw.git
    GIT_TAG 3.4
)

FetchContent_MakeAvailable(glfw)

# OpenGL
find_package(OpenGL REQUIRED)

# GLAD
add_library(glad
    glad/src/glad.c
)

target_include_directories(glad PUBLIC
    glad/include
)

# Your program
add_executable(OpenGL-Practice
    src/main.cpp
)

configure_file(
    "${CMAKE_SOURCE_DIR}/src/shader.vs"
    "${CMAKE_BINARY_DIR}/shader.vs"
    COPYONLY
)

configure_file(
    "${CMAKE_SOURCE_DIR}/src/shader.fs"
    "${CMAKE_BINARY_DIR}/shader.fs"
    COPYONLY
)

target_link_libraries(OpenGL-Practice
    PRIVATE
    glfw
    glad
    OpenGL::GL
)
