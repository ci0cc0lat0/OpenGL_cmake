cmake_minimum_required(VERSION 3.2)
# Set name of the project (for the .exe or .sln)
project(AntGL)

# Setting GLFW to the directory in which our dependencies live
set(GLFW_DIR ${CMAKE_SOURCE_DIR}/depend)

# Includes root folder and the includes folder
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${GLFW_DIR}/include)

# setting a var SOURCES to the target to be executed
set(SOURCES Source.cpp  ${GLFW_DIR}/include/glad/glad.c  ${GLFW_DIR}/include/GLFW/glfw3.h )
add_executable(${PROJECT_NAME} ${SOURCES})

# glfw3.lib is precompiled, we point the project to the library
target_link_libraries(${PROJECT_NAME} ${GLFW_DIR}/libs/glfw3.lib)


# That automatic solution
file(GLOB config_files "${CMAKE_SOURCE_DIR}/*")
foreach(file ${config_files})
    if(NOT IS_DIRECTORY ${file})
        get_filename_component(file_name ${file} NAME)
        configure_file(${file} ${CMAKE_CURRENT_BINARY_DIR}/${file_name} @ONLY)
    endif()
endforeach()


if(WIN32)
    target_link_libraries(${PROJECT_NAME} opengl32 gdi32)
endif()