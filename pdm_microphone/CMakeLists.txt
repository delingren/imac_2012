# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)

# == DO NEVER EDIT THE NEXT LINES for Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 1.5.1)
set(toolchainVersion 13_2_Rel1)
set(picotoolVersion 2.0.0)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(pdm_microphone C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(pdm_microphone 
  main.c 
  pdm_microphone.c
  usb_descriptors.c
  usb_microphone.c
  OpenPDM2PCM/OpenPDMFilter.c
  )

pico_set_program_name(pdm_microphone "pdm_microphone")
pico_set_program_version(pdm_microphone "0.1")

# Generate PIO header
pico_generate_pio_header(pdm_microphone ${CMAKE_CURRENT_LIST_DIR}/pdm_microphone.pio)

# Modify the below lines to enable/disable output over UART/USB
pico_enable_stdio_uart(pdm_microphone 0)
pico_enable_stdio_usb(pdm_microphone 0)

# Add the standard library to the build
target_link_libraries(pdm_microphone
        pico_stdlib tinyusb_common tinyusb_device tinyusb_board)

# Add the standard include files to the build
target_include_directories(pdm_microphone PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}
  ${CMAKE_CURRENT_LIST_DIR}/src/include
  ${CMAKE_CURRENT_LIST_DIR}/.. # for our common lwipopts or any other standard includes, if required
)

# Add any user requested libraries
target_link_libraries(pdm_microphone 
        hardware_pio
        hardware_dma
        )

pico_add_extra_outputs(pdm_microphone)
