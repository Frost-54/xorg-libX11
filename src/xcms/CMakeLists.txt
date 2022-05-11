add_library(x11-libxcms STATIC
      AddDIC.c 
      AddSF.c 
      CCC.c 
      CvColW.c 
      CvCols.c 
      Cv.h 
      HVC.c 
      HVCGcC.c 
      HVCGcV.c 
      HVCGcVC.c 
      HVCMnV.c 
      HVCMxC.c 
      HVCMxV.c 
      HVCMxVC.c 
      HVCMxVs.c 
      HVCWpAj.c 
      IdOfPr.c 
      LRGB.c 
      Lab.c 
      LabGcC.c 
      LabGcL.c 
      LabGcLC.c 
      LabMnL.c 
      LabMxC.c 
      LabMxL.c 
      LabMxLC.c 
      LabWpAj.c 
      Luv.c 
      LuvGcC.c 
      LuvGcL.c 
      LuvGcLC.c 
      LuvMnL.c 
      LuvMxC.c 
      LuvMxL.c 
      LuvMxLC.c 
      LuvWpAj.c 
      OfCCC.c 
      PrOfId.c 
      QBlack.c 
      QBlue.c 
      QGreen.c 
      QRed.c 
      QWhite.c 
      QuCol.c 
      QuCols.c 
      SetCCC.c 
      SetGetCols.c 
      StCol.c 
      StCols.c 
      UNDEFINED.c 
      XRGB.c 
      XYZ.c 
      cmsAllCol.c 
      cmsAllNCol.c 
      cmsCmap.c 
      cmsColNm.c 
      cmsGlobls.c 
      cmsInt.c 
      cmsLkCol.c 
      cmsMath.c 
      cmsProp.c 
      cmsTrig.c 
      uvY.c 
      xyY.c 
      Xcmsint.h
)

target_link_libraries(x11-libxcms PRIVATE x11-root-target)
target_compile_definitions(x11-libxcms PRIVATE
      XCMSDB=${X11_DATA_FILE_DEFINE_DIR}
)
add_dependencies(x11-libxcms x11-root-target)
add_custom_command(TARGET x11-libxcms
      POST_BUILD
      COMMAND cp ${CMAKE_CURRENT_LIST_DIR}/Xcms.txt ${X11_DATA_FILE_DIR}/Xcms.txt
)
execute_process(COMMAND mkdir ${X11_DATA_FILE_DIR})
