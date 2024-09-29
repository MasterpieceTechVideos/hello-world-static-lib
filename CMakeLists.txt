cmake_minimum_required(VERSION 3.5...3.30)

project(hello-world-static-lib 
    VERSION 1.0.1 
    DESCRIPTION "basic static library for saying hi :)"
    LANGUAGES CXX
)

add_library(hello_static_lib STATIC src/hello_static_lib.cpp) 

set_target_properties(hello_static_lib PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
    PUBLIC_HEADER ${CMAKE_CURRENT_LIST_DIR}/include/hello_static_lib.h) 
target_include_directories(hello_static_lib PRIVATE ${CMAKE_CURRENT_LIST_DIR}/include)

add_custom_command(TARGET hello_static_lib 
    POST_BUILD COMMAND ${CMAKE_COMMAND} -E 
    copy_if_different ${CMAKE_CURRENT_LIST_DIR}/include/hello_static_lib.h  
    $<TARGET_FILE_DIR:hello_static_lib>) 