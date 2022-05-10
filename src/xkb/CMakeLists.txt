add_library(x11-libxkb
      XKB.c 
      XKBBind.c 
      XKBCompat.c 
      XKBCtrls.c 
      XKBCvt.c 
      XKBGetMap.c 
      XKBGetByName.c 
      XKBNames.c 
      XKBRdBuf.c 
      XKBSetMap.c 
      XKBUse.c 
      XKBleds.c 
      XKBBell.c 
      XKBGeom.c 
      XKBSetGeom.c 
      XKBExtDev.c 
      XKBList.c 
      XKBMisc.c 
      XKBMAlloc.c 
      XKBGAlloc.c 
      XKBAlloc.c 
      XKBlibint.h
)

target_include_directories(x11-libxkb PRIVATE ${X11_INCLUDE_DIRS})
target_compile_definitions(x11-libxkb PRIVATE _BSD_SOURCE)
