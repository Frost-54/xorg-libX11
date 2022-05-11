project(xorg-libx11)

include(CheckCSourceCompiles)
check_c_source_compiles(
      "#include <X11/Xthreads.h>\n int main() {}"
      HAS_XTHREADS
)

set(XUSE_MTSAFE_API ${HAS_XTHREADS})

add_compile_definitions(WCHAR32=1 HAVE_CONFIG_H)
# Check xthreads?
add_compile_definitions(XTHREADS XUSE_MTSAFE_API)

include(CheckIncludeFile)
CHECK_INCLUDE_FILE("sys/filio.h" HAVE_SYS_FILIO_H)
if(HAVE_SYS_FILIO_H)
      add_compile_definitions(HAVE_SYS_FILIO_H)
endif()

CHECK_INCLUDE_FILE("sys/socket.h" HAVE_SYS_SOCKET_H)
if(HAVE_SYS_SOCKET_H)
      add_compile_definitions(HAVE_SYS_SOCKET_H)
endif()

CHECK_INCLUDE_FILE("unistd.h" HAVE_UNISTD_H)
if(HAVE_UNISTD_H)
      add_compile_definitions(HAVE_UNISTD_H)
endif()

CHECK_INCLUDE_FILE("sys/ioctl.h" HAVE_SYS_IOCTL_H)
if(HAVE_SYS_IOCTL_H)
      add_compile_definitions(HAVE_SYS_IOCTL_H)
endif()

CHECK_INCLUDE_FILE("inttypes.h" HAVE_INTTYPES_H)
if(HAVE_INTTYPES_H)
      add_compile_definitions(HAVE_INTTYPES_H)
endif()

CHECK_INCLUDE_FILE("sys/select.h" HAVE_SYS_SELECT_H)
if(HAVE_SYS_SELECT_H)
      add_compile_definitions(HAVE_SYS_SELECT_H)
endif()

CHECK_INCLUDE_FILE("dlfcn.h" HAVE_LOADABLE_MODULES)
if(HAVE_LOADABLE_MODULES)
      add_compile_definitions(HAVE_LOADABLE_MODULES HAVE_DLFCN_H)
endif()

CHECK_INCLUDE_FILE("dl.h" HAVE_DL_H)
if(HAVE_DL_H)
      add_compile_definitions(HAVE_LOADABLE_MODULES HAVE_DL_H)
endif()

include(CheckFunctionExists)
check_function_exists(issetugid HAVE_ISSETGUID)
if (HAVE_ISSETGUID)
      add_compile_definitions(HAVE_ISSETGUID)
endif()

check_function_exists(getresuid HAVE_GETRESUID)
if (HAVE_GETRESUID)
      add_compile_definitions(HAVE_GETRESUID)
endif()

check_function_exists(shmat HAVE_SHMAT)
if (HAVE_SHMAT)
      add_compile_definitions(HAVE_SHMAT)
endif()

###################### Data files #######################3
# X11_DATA_FILE_DIR is the directory where cmake copy files to
if (NOT X11_DATA_FILE_DIR)
      set(X11_DATA_FILE_DIR "${CMAKE_BINARY_DIR}")
endif()
# X11_DATA_FILE_DEFINE_DIR is the directory for your executable to find data files
if (NOT X11_DATA_FILE_DEFINE_DIR)
      set(X11_DATA_FILE_DEFINE_DIR "${CMAKE_BINARY_DIR}")
endif()

configure_file(
      ${CMAKE_CURRENT_LIST_DIR}/config/config.h.in 
      ${CMAKE_CURRENT_BINARY_DIR}/X11/XlibConf.h
)

configure_file(
      ${CMAKE_CURRENT_LIST_DIR}/config/config.h.in 
      ${CMAKE_CURRENT_BINARY_DIR}/config.h
)

# add_dependencies(x11-root-target, ...) to force command to run before building X11 libraries
add_library(x11-root-target INTERFACE

)

target_include_directories(x11-root-target INTERFACE 
      ${CMAKE_CURRENT_SOURCE_DIR}/include
      ${CMAKE_CURRENT_SOURCE_DIR}/include/X11
      ${CMAKE_CURRENT_SOURCE_DIR}/src/xcms
      ${CMAKE_CURRENT_SOURCE_DIR}/src/xkb
      ${CMAKE_CURRENT_SOURCE_DIR}/src/xlibi18n
      ${CMAKE_CURRENT_SOURCE_DIR}/src

      # Note: add a custom rule in your project to clone 
      # https://github.com/freedesktop/xorg-xorgproto.git
      # https://github.com/freedesktop/xcb-libxcb.git xorg-libX11/external/xcb-libxcb
      # https://github.com/xkbcommon/libxkbcommon.git
      ${CMAKE_CURRENT_LIST_DIR}/external/xorg-xorgproto/include
      ${CMAKE_CURRENT_LIST_DIR}/external/xcb-libxcb/src
      ${CMAKE_CURRENT_LIST_DIR}/external/xorg-libxtrans
      ${CMAKE_CURRENT_LIST_DIR}/external/libxkbcommon/src
      ${CMAKE_CURRENT_LIST_DIR}/external/libxkbcommon/include

      ${CMAKE_CURRENT_BINARY_DIR}/include
      ${CMAKE_CURRENT_BINARY_DIR}/include/X11
      ${CMAKE_CURRENT_BINARY_DIR}

      ${CMAKE_CURRENT_BINARY_DIR}/external/xorg-xorgproto/include
)

set(X11_PROTOCOL_PATH ${CMAKE_CURRENT_LIST_DIR}/external/xorg-xorgproto)

add_subdirectory(src)
add_subdirectory(modules)
add_subdirectory(external/xcb-libxcb)
