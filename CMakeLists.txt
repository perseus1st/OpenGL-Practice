cmake_minimum_required(VERSION 3.20)

project(Alexandria-2 LANGUAGES C CXX)

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
add_executable(Alexandria-2
    main.cpp
)

target_link_libraries(Alexandria-2
    PRIVATE
    glfw
    glad
    OpenGL::GL
)
