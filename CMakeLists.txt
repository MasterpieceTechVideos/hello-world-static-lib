cmake_minimum_required(VERSION 3.5...3.30)

project(hello-world-static-lib 
    VERSION 1.0.1 
    DESCRIPTION "basic static library for saying hi :)"
    LANGUAGES CXX
)

add_library(hello-static-lib STATIC src/hello-static-lib.cpp) 

set_target_properties(hello-static-lib PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
    PUBLIC_HEADER ${CMAKE_CURRENT_LIST_DIR}/include/hello-static-lib.h) 
target_include_directories(hello-static-lib PRIVATE ${CMAKE_CURRENT_LIST_DIR}/include)

add_custom_command(TARGET hello-static-lib 
    POST_BUILD COMMAND ${CMAKE_COMMAND} -E 
    copy_if_different ${CMAKE_CURRENT_LIST_DIR}/include/hello-static-lib.h  
    $<TARGET_FILE_DIR:hello-static-lib>) 