cmake_minimum_required(VERSION 3.16)

if (DEFINED ESP_PLATFORM)
  # idf component
  idf_component_register(
      SRCS src/sbc/sbc.c src/sbc/sbc_primitives.c
      INCLUDE_DIRS src
  )

  # No -DARDUINO here (unlike the non-idf branch below): it would leak PUBLIC
  # into every component that REQUIRES codec-sbc (ESP32-A2DP, main),
  # making arduino-audio-tools/AudioToolsConfig.h think it's building against
  # the real Arduino framework (pulling in Arduino.h, expecting delay()/
  # millis()/etc.) when this is a plain esp-idf project. src/sbc/formats.h
  # and sbc_primitives.h fall back to <byteswap.h>/inline without it, and
  # the esp-idf toolchain's picolibc provides <byteswap.h>, so that fallback
  # works fine here.
  target_compile_options(${COMPONENT_LIB} PRIVATE -Wno-error -Wno-double-promotion -Wno-ignored-attributes)

else()

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

endif()
