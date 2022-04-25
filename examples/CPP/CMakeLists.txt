# This is the project CMakeLists.txt file for an example project
cmake_minimum_required(VERSION 3.5)
# Include the DHT component
# NOTE: The EXTRA_COMPONENT_DIRS folder must be named explicitly for some 
# reason, maybe because the end of the string is directly parsed by the tool 
# (not converted with fullpath then parsed).
# "../../" will not work.  Not sure why.
set(EXTRA_COMPONENT_DIRS "../../../DHT22-lib-for-esp-idf")
include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(DHT22-example-CPP)



