set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_VERSION 1)
cmake_minimum_required(VERSION 3.17)

########################################################################################################################
# Project settings - USER MUST CONFIG
########################################################################################################################
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD 11)
set(LINKER_SCRIPT_NAME STM32L476RGTX_FLASH.ld)
set(COMPILER_DEFINITIONS "-DUSE_HAL_DRIVER -DSTM32L476xx")
########################################################################################################################

########################################################################################################################
# TOOLCHAIN Settings
########################################################################################################################
# Toolchain configuration
set(CMAKE_C_COMPILER arm-none-eabi-gcc)
set(CMAKE_CXX_COMPILER arm-none-eabi-g++)
set(CMAKE_ASM_COMPILER  arm-none-eabi-gcc)
set(CMAKE_AR arm-none-eabi-ar)
set(CMAKE_OBJCOPY arm-none-eabi-objcopy)
set(CMAKE_OBJDUMP arm-none-eabi-objdump)
set(SIZE arm-none-eabi-size)
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)
########################################################################################################################

project(STM32-Template C CXX ASM)

########################################################################################################################
# COMPILER
########################################################################################################################
# Compilation options
add_compile_options(-mcpu=cortex-m4 -mthumb -mthumb-interwork)
add_compile_options(-ffunction-sections -fdata-sections -fno-common -fmessage-length=0)
if ("${CMAKE_BUILD_TYPE}" STREQUAL "Release")
    message(STATUS "Maximum optimization for speed")
    add_compile_options(-Ofast)
elseif ("${CMAKE_BUILD_TYPE}" STREQUAL "RelWithDebInfo")
    message(STATUS "Maximum optimization for speed, debug info included")
    add_compile_options(-Ofast -g)
    add_definitions(-DDEBUG)
elseif ("${CMAKE_BUILD_TYPE}" STREQUAL "MinSizeRel")
    message(STATUS "Maximum optimization for size")
    add_compile_options(-Os)
else ()
    message(STATUS "Minimal optimization, debug info included")
    add_compile_options(-Og -g)
    add_definitions(-DDEBUG)
endif ()
# Compiler definitions
add_definitions(${COMPILER_DEFINITIONS})

########################################################################################################################
# LINKER
########################################################################################################################
# Linker script directory
set(LINKER_SCRIPT_PATH ${CMAKE_SOURCE_DIR}/Scripts/Linker)
# Linker script
set(LINKER_SCRIPT ${LINKER_SCRIPT_PATH}/${LINKER_SCRIPT_NAME})
# Linker options
add_link_options(-Wl,-gc-sections,--print-memory-usage,-Map=${PROJECT_BINARY_DIR}/${PROJECT_NAME}.map)
add_link_options(-mcpu=cortex-m4 -mthumb -mthumb-interwork)
add_link_options(-T ${LINKER_SCRIPT})
########################################################################################################################

########################################################################################################################
# DEPENDENCIES
########################################################################################################################
# Core directory for microcontroller
add_subdirectory(Core)