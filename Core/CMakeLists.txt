# Core project
project(core)

# HAL Configuration file
set(CORE_CONFIGURATION_HEADERS Configuration/stm32l4xx_hal_conf.h)
# Source files of system core
file(GLOB_RECURSE SOURCE_FILES "System/Source/*.c" "System/Startup/*.s")
# Core driver library
add_subdirectory(Drivers)
add_subdirectory(Configuration)

add_executable(${PROJECT_NAME}.elf ${SOURCE_FILES} ${LINKER_SCRIPT})

target_include_directories(${PROJECT_NAME}.elf PUBLIC System/Include)
target_include_directories(${PROJECT_NAME}.elf PRIVATE System/Source)
target_include_directories(${PROJECT_NAME}.elf PRIVATE System/Startup)
target_link_libraries(${PROJECT_NAME}.elf PUBLIC armdrivers configuration)

set(HEX_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.hex)
set(BIN_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.bin)

add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} -Oihex $<TARGET_FILE:${PROJECT_NAME}.elf> ${HEX_FILE}
        COMMAND ${CMAKE_OBJCOPY} -Obinary $<TARGET_FILE:${PROJECT_NAME}.elf> ${BIN_FILE}
        COMMENT "Building ${HEX_FILE}
Building ${BIN_FILE}")

#add_subdirectory(Configuration)
#add_subdirectory(Drivers)
#add_subdirectory(System)
#add_subdirectory(Core)