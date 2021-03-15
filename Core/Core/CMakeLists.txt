project(core)

# List of source files to be compiled.
file(GLOB_RECURSE SOURCE_FILES "Source/*.c" "Startup/*.s")

add_executable(${PROJECT_NAME}.elf ${SOURCE_FILES} ${LINKER_SCRIPT})

target_include_directories(${PROJECT_NAME}.elf PUBLIC Include)
target_include_directories(${PROJECT_NAME}.elf PRIVATE Source)
target_include_directories(${PROJECT_NAME}.elf PRIVATE Startup)
target_link_libraries(${PROJECT_NAME}.elf PUBLIC armdrivers)

set(HEX_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.hex)
set(BIN_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.bin)

add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} -Oihex $<TARGET_FILE:${PROJECT_NAME}.elf> ${HEX_FILE}
        COMMAND ${CMAKE_OBJCOPY} -Obinary $<TARGET_FILE:${PROJECT_NAME}.elf> ${BIN_FILE}
        COMMENT "Building ${HEX_FILE}
Building ${BIN_FILE}")