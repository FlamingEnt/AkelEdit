cmake_minimum_required(VERSION 3.0.0)
project(AkelEdit)

if(CMAKE_SIZEOF_VOID_P MATCHES "8")
  set(BIT "64")
else()
  set(BIT "32")
endif()

add_compile_definitions(RC_AKELEDITBIT=${BIT})
add_compile_definitions(BIT=${BIT})

if(MSVC)
  add_compile_options(/wd4100 /wd4191 /wd4201 /wd4204 /wd4255 /wd4310 /wd4619 /wd4668 /wd4701 /wd4706 /wd4711 /wd4820 /wd4826)
endif()

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
  SHARED
  ${SOURCES}
)

target_link_libraries(AkelEdit
  uuid
  imm32
  ole32
  gdi32
)

install(TARGETS AkelEdit
  RUNTIME DESTINATION ${UNREAL_BIN_PATH}
  LIBRARY DESTINATION ${UNREAL_BIN_PATH}
)