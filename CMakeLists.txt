cmake_minimum_required(VERSION 3.5)
include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(DHT22-lib-for-esp-idf)

# idf_component_register(SRCS "src/DHT_c.c" "src/DHT.cpp" 
#                     INCLUDE_DIRS "include")

add_library(DHT22-lib-for-esp-idf "src/DHT_c.c" "src/DHT.cpp")
target_include_directories(DH22-lib-for-esp-idf 
    INTERFACE ${PROJECT_SOURCE_DIR}/include)
    
add_subdirectory(examples)
add_subdirectory(fwtest)
