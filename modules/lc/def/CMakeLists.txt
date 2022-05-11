add_library(x11-xlcDef STATIC 
      lcDefConv.c
)
target_link_libraries(x11-xlcDef PRIVATE x11-root-target)
add_dependencies(x11-xlcDef x11-root-target)
