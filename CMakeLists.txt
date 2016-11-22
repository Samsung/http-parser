cmake_minimum_required(VERSION 2.8)

PROJECT(http-parser C)

set(targetName httpparser)

INCLUDE_DIRECTORIES(./)

if(NOT${BUILDTYPE})
  set(BUILDTYPE "Debug")
endif()


if(${OS} STREQUAL "NUTTX")
  set(TARGET_INCLUDE "${NUTTX_HOME}/include")
  set(TARGET_INCLUDE ${TARGET_INCLUDE} "${NUTTX_HOME}/include/cxx")
  INCLUDE_DIRECTORIES(./ ${TARGET_INCLUDE})
endif()

set(CFLAGS "${CFLAGS} ${CMAKE_CXX_FLAGS}")


if("${BUILDTYPE}" STREQUAL "Release")
  set(CFLAGS "${CFLAGS} -Os")
else()
  set(CFLAGS "${CFLAGS} -g")
endif()

ADD_LIBRARY(${targetName} STATIC http_parser.c)
set_target_properties(${targetName} PROPERTIES COMPILE_FLAGS ${CFLAGS})
