cmake_minimum_required(VERSION 3.2)
# Set name of the project (for the .exe or .sln)
project(AntGL)

# Setting GLFW to the directory in which our dependencies live
set(GLFW_DIR ${CMAKE_SOURCE_DIR}/depend)



# Includes root folder and the includes folder
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${GLFW_DIR}/include)

# may not be needed, as the source.cpp looks like glad/glad.h
#include_directories(${GLFW_DIR}/include/glad) 

# setting a var SOURCES to the target to be executed
set(SOURCES Source.cpp  ${GLFW_DIR}/include/glad/glad.c  ${GLFW_DIR}/include/GLFW/glfw3.h )

add_executable(${PROJECT_NAME} ${SOURCES})

# glfw3.lib is precompiled, we point the project to the library
target_link_libraries(${PROJECT_NAME} ${GLFW_DIR}/libs/glfw3.lib)

# Ideally, I would have something automatic to read the files from the src/root folder and shove them into the bin directory
configure_file(vert_shader.vs ${CMAKE_CURRENT_BINARY_DIR}/vert_shader.vs COPYONLY)
configure_file(frag_shader.fs ${CMAKE_CURRENT_BINARY_DIR}/frag_shader.fs COPYONLY)
configure_file(TextFile1.txt ${CMAKE_CURRENT_BINARY_DIR}/TextFile1.txt COPYONLY)




if(WIN32)
    target_link_libraries(${PROJECT_NAME} opengl32 gdi32)
endif()