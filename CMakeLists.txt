cmake_minimum_required(VERSION 3.27.2 FATAL_ERROR)

project(2dgameengine VERSION 1.0.0 LANGUAGES CXX)
add_executable(${PROJECT_NAME} ${CMAKE_SOURCE_DIR}/src/main.cpp)

add_subdirectory(${CMAKE_SOURCE_DIR}/vendor/glad)
add_subdirectory(${CMAKE_SOURCE_DIR}/vendor/glfw)

find_package(OpenGL REQUIRED)

list(
    APPEND
    INCLUDE_PATHS
    "${CMAKE_SOURCE_DIR}/vendor/glad/include"
    "${CMAKE_SOURCE_DIR}/vendor/glfw-3.3.8/include"
)
target_include_directories(${PROJECT_NAME} PUBLIC "$<BUILD_INTERFACE:${INCLUDE_PATHS}>")
target_link_libraries(${PROJECT_NAME} ${OPENGL_LIBRARIES} glfw glad)

set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin/debug)
