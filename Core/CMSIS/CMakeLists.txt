project(cmsis)

# Include paths for this library
set(CMSIS_DEVICE_INCLUDE_PATH Device/ST/STM32L4xx/Include)
set(CMSIS_CORE_INCLUDE_PATH Include)

# Create target library
add_library(${PROJECT_NAME} INTERFACE)
# Append include directories to library
target_include_directories(${PROJECT_NAME} INTERFACE ${CMSIS_DEVICE_INCLUDE_PATH})
target_include_directories(${PROJECT_NAME} INTERFACE ${CMSIS_CORE_INCLUDE_PATH})


