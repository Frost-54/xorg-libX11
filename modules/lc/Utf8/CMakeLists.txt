add_library(x11-xlcUTF8Load STATIC
      lcUTF8Load.c
)
target_link_libraries(x11-xlcUTF8Load PRIVATE x11-root-target)
add_dependencies(x11-xlcUTF8Load x11-root-target)
