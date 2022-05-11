add_executable(x11-makekeys makekeys.c)
target_link_libraries(x11-makekeys x11-root-target)
add_dependencies(x11-makekeys x11-root-target)

