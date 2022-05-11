add_library(x11-ximcp STATIC
      imCallbk.c 
      imDefFlt.c 
      imDefIc.c 
      imDefIm.c 
      imDefLkup.c 
      imDispch.c 
      imEvToWire.c 
      imExten.c 
      imImSw.c 
      imInsClbk.c 
      imInt.c 
      imLcFlt.c 
      imLcGIc.c 
      imLcIc.c 
      imLcIm.c 
      imLcLkup.c 
      imLcPrs.c 
      imLcSIc.c 
      imRmAttr.c 
      imRm.c 
      imThaiFlt.c 
      imThaiIc.c 
      imThaiIm.c 
      imTrans.c 
      imTransR.c 
      imTrX.c
      ${XIMCP_SOURCES}
)

target_link_libraries(x11-ximcp PRIVATE
      x11-root-target
)

target_compile_definitions(x11-ximcp PRIVATE
      BSD_SOURCE XIM_t TRANS_CLIENT
)

add_dependencies(x11-ximcp x11-root-target)
