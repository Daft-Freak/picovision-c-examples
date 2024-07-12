cmake_minimum_required(VERSION 3.12)

set(NAME picovision-boilerplate)  # TODO: Change me!

include(pimoroni_pico_import.cmake)
include(pico_sdk_import.cmake)

# Gooey boilerplate
project(${NAME} C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialize the SDK
pico_sdk_init()

include(picovision_import.cmake)

# Include required libraries
# This assumes `pimoroni-pico` is stored alongside your project

# I2C and SPI
include(common/pimoroni_i2c)
include(common/pimoroni_bus)

# Graphics stuff
include(libraries/jpegdec/jpegdec)
include(libraries/pico_graphics/pico_graphics)

# SD Card Access
include(drivers/fatfs/fatfs)
include(drivers/sdcard/sdcard)

include(dv_stick_test.cmake)
include(dv_sprite_test.cmake)
include(dv_slideshow.cmake)

# Set up files for the release packages
install(FILES
    ${CMAKE_CURRENT_LIST_DIR}/README.md
    DESTINATION .
)

set(CPACK_INCLUDE_TOPLEVEL_DIRECTORY OFF)
set(CPACK_GENERATOR "ZIP" "TGZ")
include(CPack)
