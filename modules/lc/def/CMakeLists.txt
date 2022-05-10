add_library(x11-xlcDef STATIC 
      lcDefConv.c
)
target_include_directories(x11-xlcDef PRIVATE ${X11_INCLUDE_DIRS})

