cmake_minimum_required(VERSION 3.16)

# set the project name
project(arduino_libsbc)

# lots of warnings and all warnings as errors
## add_compile_options(-Wall -Wextra )
set(CMAKE_CXX_STANDARD 17)

# define libraries
add_library (arduino_libsbc 
    "${PROJECT_SOURCE_DIR}/src/sbc/sbc.c"
    "${PROJECT_SOURCE_DIR}/src/sbc/sbc_primitives.c"
)

target_compile_options(arduino_libsbc PRIVATE  -Wdouble-promotion -Wno-ignored-attributes)
target_compile_definitions(arduino_libsbc PUBLIC -DARDUINO)

# define location for header files
target_include_directories(arduino_libsbc PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src )
