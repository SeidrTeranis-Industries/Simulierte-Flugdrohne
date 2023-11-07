cmake_minimum_required(VERSION 3.0)
project(Drohnensteuerung)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(OpenGL_GL_PREFERENCE "GLVND")

find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)
find_package(GLEW REQUIRED)

include_directories("./imgui")

set(SOURCES
    src/main.cpp
    src/drone.cpp
)

set(HEADERS
    include/drone.hpp
    imgui/backends/imgui_impl_glfw.h
    imgui/backends/imgui_impl_opengl3.h
)

set(IMGUI_SOURCES
    imgui/imgui.cpp
    imgui/imgui_draw.cpp
    imgui/imgui_widgets.cpp
    imgui/imgui_tables.cpp
    imgui/backends/imgui_impl_glfw.cpp
    imgui/backends/imgui_impl_opengl3.cpp
)

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS} ${IMGUI_SOURCES})

# Link OPENGL
target_link_libraries(${PROJECT_NAME} OpenGL::GL)

# Link GLFW and GLEW
target_link_libraries(${PROJECT_NAME} glfw GLEW::GLEW)

file(COPY assets DESTINATION ${CMAKE_BINARY_DIR})

