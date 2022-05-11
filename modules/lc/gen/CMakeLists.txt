add_library(x11-libxlibi18n STATIC
      lcGenConv.c
)
target_link_libraries(x11-libxlibi18n PRIVATE x11-root-target)
add_dependencies(x11-libxlibi18n x11-root-target)

