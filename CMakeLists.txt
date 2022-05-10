project(xorg-libx11)

include(CheckCSourceCompiles)
check_c_source_compiles(
      "#include <X11/Xthreads.h>\n int main() {}"
      HAS_XTHREADS
)

set(XUSE_MTSAFE_API ${HAS_XTHREADS})

add_compile_definitions(WCHAR32=1)

configure_file(
      ${CMAKE_CURRENT_LIST_DIR}/config/config.h.in 
      ${CMAKE_CURRENT_BINARY_DIR}/X11/XlibConf.h
)

configure_file(
      ${CMAKE_CURRENT_LIST_DIR}/config/config.h.in 
      ${CMAKE_CURRENT_BINARY_DIR}/config.h
)

list(APPEND X11_INCLUDE_DIRS 
      ${CMAKE_CURRENT_SOURCE_DIR}/include
      ${CMAKE_CURRENT_SOURCE_DIR}/include/X11
      ${CMAKE_CURRENT_SOURCE_DIR}/src/xcms
      ${CMAKE_CURRENT_SOURCE_DIR}/src/xkb
      ${CMAKE_CURRENT_SOURCE_DIR}/src/xlibi18n

      # Note: add a custom rule in your project to clone 
      # https://github.com/freedesktop/xorg-xorgproto.git
      # https://github.com/freedesktop/xcb-libxcb.git xorg-libX11/external/xcb-libxcb
      # https://github.com/xkbcommon/libxkbcommon.git
      ${CMAKE_CURRENT_LIST_DIR}/external/xorg-xorgproto/include
      ${CMAKE_CURRENT_LIST_DIR}/external/xcb-libxcb/src

      ${CMAKE_CURRENT_BINARY_DIR}/include
      ${CMAKE_CURRENT_BINARY_DIR}/include/X11
      ${CMAKE_CURRENT_BINARY_DIR}
)

add_subdirectory(src)
add_subdirectory(modules)
