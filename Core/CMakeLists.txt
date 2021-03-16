# Core project
project(core)

# Source files of system core
file(GLOB_RECURSE SOURCE_FILES "System/Source/*.c" "System/Startup/*.s")
# Core driver library
add_subdirectory(CMSIS)
add_subdirectory(HALDrivers)
add_subdirectory(Configuration)

add_executable(${PROJECT_NAME}.elf ${SOURCE_FILES} ${LINKER_SCRIPT})

target_include_directories(${PROJECT_NAME}.elf PUBLIC System/Include)
target_link_libraries(${PROJECT_NAME}.elf PUBLIC cmsis haldrivers configuration)

set(HEX_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.hex)
set(BIN_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.bin)

add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} -Oihex $<TARGET_FILE:${PROJECT_NAME}.elf> ${HEX_FILE}
        COMMAND ${CMAKE_OBJCOPY} -Obinary $<TARGET_FILE:${PROJECT_NAME}.elf> ${BIN_FILE}
        COMMENT "Building ${HEX_FILE}
Building ${BIN_FILE}")