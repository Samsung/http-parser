cmake_minimum_required(VERSION 2.8)

PROJECT(http-parser)

set(targetName httpparser)

INCLUDE_DIRECTORIES(./)

if(NOT${BUILDTYPE})
  set(BUILDTYPE "Debug")
endif()


if(${OS} STREQUAL "NUTTX")
  set(TARGET_INCLUDE "${NUTTX_HOME}/include")
  set(TARGET_INCLUDE ${TARGET_INCLUDE} "${NUTTX_HOME}/include/cxx")
  INCLUDE_DIRECTORIES(./ ${TARGET_INCLUDE})

  set(FLAGS_NUTTX
    -mcpu=cortex-m4
    -mthumb
    -march=armv7e-m
    -mfpu=fpv4-sp-d16
    -mfloat-abi=hard
    -D__NUTTX__
    -D__ARM__
    -Os
    -fno-strict-aliasing
    -fno-strength-reduce
    -fomit-frame-pointer)
  set(CFLAGS "${FLAGS_NUTTX}")
endif()


if("${BUILDTYPE}" STREQUAL "Release")
  set(CFLAGS "${CFLAGS} -Os")
else()
  set(CFLAGS "${CFLAGS} -g")
endif()

ADD_LIBRARY(${targetName} STATIC http_parser.c)
set_target_properties(${targetName} PROPERTIES COMPILE_FLAGS ${CFLAGS})
