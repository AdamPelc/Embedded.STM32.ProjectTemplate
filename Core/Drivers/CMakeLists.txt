# ARM Cortex Drivers library
project(armdrivers)

# Internal paths variables for this library.
set(HAL_INCLUDE_PATH STM32L4xx_HAL_Driver/Inc)
set(CMSIS_DEVICE_INCLUDE_PATH CMSIS/Device/ST/STM32L4xx/Include)
set(CMSIS_CORE_INCLUDE_PATH CMSIS/Include)
set(HAL_SOURCE_PATH STM32L4xx_HAL_Driver/Src)

# List of source files to be compiled.
file(GLOB_RECURSE SOURCE_FILES ${HAL_SOURCE_PATH}/*.c)
file(GLOB_RECURSE HAL_INCLUDE_FILES ${HAL_INCLUDE_PATH}/*.h)

# Create target library
add_library(${PROJECT_NAME} ${SOURCE_FILES} ${HAL_INCLUDE_FILES})

# Append directories to library
target_include_directories(${PROJECT_NAME} PUBLIC ${HAL_INCLUDE_PATH})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMSIS_DEVICE_INCLUDE_PATH})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMSIS_CORE_INCLUDE_PATH})
target_include_directories(${PROJECT_NAME} PRIVATE ${HAL_SOURCE_PATH})

# Add configuration library
target_link_libraries(${PROJECT_NAME} PUBLIC configuration)

