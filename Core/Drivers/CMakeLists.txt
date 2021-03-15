# ARM Cortex Drivers library
project(armdrivers)

# Path variables for this library.
set(HAL_INCLUDE_PATH STM32L4xx_HAL_Driver/Inc)
set(CMSIS_DEVICE_INCLUDE_PATH CMSIS/Device/ST/STM32L4xx/Include)
set(CMSIS_CORE_INCLUDE_PATH CMSIS/Include)
set(HAL_SOURCE_PATH STM32L4xx_HAL_Driver/Src)

# List of public header interfaces of this library.
# set(HEADERS_FILES ${HAL_INCLUDE_PATH}/stm32l4xx_hal.h)
# List of source files
file(GLOB_RECURSE SOURCE_FILES ${HAL_SOURCE_PATH}/*.c)

# Create target library
add_library(${PROJECT_NAME} ${HEADERS_FILES} ${SOURCE_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC ${HAL_INCLUDE_PATH})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMSIS_DEVICE_INCLUDE_PATH})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMSIS_CORE_INCLUDE_PATH})
target_include_directories(${PROJECT_NAME} PRIVATE ${HAL_SOURCE_PATH})


