cmake_minimum_required(VERSION 3.0.0)
project(AkelEdit)

if(CMAKE_SIZEOF_VOID_P MATCHES "8")
  set(BIT "64")
else()
  set(BIT "32")
endif()

add_compile_definitions(RC_AKELEDITBIT=${BIT})

set(SOURCES
  "AkelEdit.c"
  "Resources/AkelEdit.rc"
)

set(HEADERS
  "AkelBuild.h"
  "AkelEdit.h"
  "RegExpFunc.h"
  "StackFunc.h"
  "StrFunc.h"
  "x64Func.h"
)

add_library(AkelEdit
  STATIC
  ${SOURCES}
)

set_target_properties(AkelEdit
  PROPERTIES
  PUBLIC_HEADER "${HEADERS}"
)

target_link_libraries(AkelEdit
  uuid
  imm32
  ole32
  gdi32
)