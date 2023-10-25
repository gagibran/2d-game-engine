cmake_minimum_required(VERSION 3.27.2 FATAL_ERROR)

project(2dgameengine VERSION 0.1.0 LANGUAGES CXX)
add_executable(${PROJECT_NAME} ${CMAKE_SOURCE_DIR}/src/main.cpp)
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_20)

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
