# This is the project CMakeLists.txt file for an example project
cmake_minimum_required(VERSION 3.5)
# include the DHT component
# NOTE: The folder must be named explicitly for some reason,
# "../../" will not work.  Not sure why.
set(EXTRA_COMPONENT_DIRS "../../../DHT22-lib-for-esp-idf")
include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(DHT22-example-C)



