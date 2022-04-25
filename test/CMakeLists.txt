# This folder is named "test" to conform to the unity / esp-idf requirement that components
# place their tests in this folder.
# However, to build the test, build the executable in the directory "fwtest".
# See https://github.com/espressif/esp-idf/tree/master/examples/system/unit_test
# And https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/unit-tests.html
idf_component_register(SRC_DIRS "."
                    INCLUDE_DIRS "."
                    REQUIRES unity DHT22-lib-for-esp-idf)
