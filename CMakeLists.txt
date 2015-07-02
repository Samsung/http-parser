cmake_minimum_required(VERSION 2.8)

PROJECT(http-parser)

#add_custom_target(httpparser)
set(targetName httpparser)

INCLUDE_DIRECTORIES(./)

if(NOT${BUILDTYPE})
  set(BUILDTYPE "Debug")
endif()

if("${BUILDTYPE}" STREQUAL "Release")
  set(CFLAGS "-Os")
else()
  set(CFLAGS "-g")
endif()

ADD_LIBRARY(${targetName} STATIC http_parser.c)
set_target_properties(${targetName} PROPERTIES COMPILE_FLAGS ${CFLAGS})
