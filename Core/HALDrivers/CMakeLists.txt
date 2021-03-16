project(haldrivers)

# List of source files
file(GLOB_RECURSE SOURCE_FILES "Src/*.c")
# Create target library
add_library(${PROJECT_NAME} ${SOURCE_FILES})
# Append directories to library
target_include_directories(${PROJECT_NAME} PUBLIC Inc)
# Add configuration library
target_link_libraries(${PROJECT_NAME} PRIVATE configuration cmsis)
