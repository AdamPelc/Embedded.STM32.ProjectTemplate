# Project configuration
project(configuration)

# Public configuration header files
set(CONFIGURATION_PUBLIC_HEADERS
        stm32l4xx_hal_conf.h
        main.h)

# Create configuration static library
add_library(${PROJECT_NAME} ${CONFIGURATION_PUBLIC_HEADERS})

# Set interface files
target_include_directories(${PROJECT_NAME} INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})
set_target_properties(${PROJECT_NAME} PROPERTIES LINKER_LANGUAGE C)