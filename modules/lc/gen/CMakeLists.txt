add_library(x11-libxlibi18n STATIC
      lcGenConv.c
)
target_include_directories(x11-libxlibi18n PRIVATE ${X11_INCLUDE_DIRS})
