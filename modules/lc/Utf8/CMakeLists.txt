add_library(x11-xlcUTF8Load STATIC
      lcUTF8oad.c
)
target_include_directories(x11-xlcUTF8Load PRIVATE ${X11_INCLUDE_DIRS})
