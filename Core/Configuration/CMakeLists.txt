# Project configuration
project(configuration)

# Create configuration static library
add_library(${PROJECT_NAME} stm32l4xx_hal_conf.h)

# Set interface files
target_include_directories(${PROJECT_NAME} INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})
set_target_properties(${PROJECT_NAME} PROPERTIES LINKER_LANGUAGE C)