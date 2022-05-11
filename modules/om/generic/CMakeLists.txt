add_library(x11-xomGeneric STATIC
      omDefault.c
      omGeneric.c
      omImText.c
      omText.c
      omTextEsc.c
      omTextExt.c
      omTextPer.c
      omXChar.c
)

target_link_libraries(x11-xomGeneric PRIVATE x11-root-target)
add_dependencies(x11-xomGeneric x11-root-target)
