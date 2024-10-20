cmake_minimum_required(VERSION 3.22)
project(vterm
  LANGUAGES C
  DESCRIPTION "Abstract VT220/Xterm/ECMA-48 emulation library"
  VERSION 0.3.3)

include_directories(include src)
add_library(${PROJECT_NAME} STATIC
  src/vterm.c
  src/pen.c
  src/unicode.c
  src/encoding.c
  src/screen.c
  src/state.c
  src/parser.c
  src/mouse.c
  src/keyboard.c
  src/rect.h
  src/utf8.h
  src/vterm_internal.h
  src/fullwidth.inc
  include/vterm.h
  include/vterm_keycodes.h
)

target_link_libraries(${PROJECT_NAME})

configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_NAME}.pc.in
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.pc)

INSTALL(FILES include/vterm.h include/vterm_keycodes.h          DESTINATION include)
INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/lib${PROJECT_NAME}.a  DESTINATION lib)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.pc    DESTINATION share/pkgconfig)
