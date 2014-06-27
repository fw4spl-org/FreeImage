
set( LIBJPEG_SOURCES 
    jaricom.c jcapimin.c jcapistd.c jcarith.c jccoefct.c 
    jccolor.c jcdctmgr.c jchuff.c jcinit.c jcmainct.c jcmarker.c 
    jcmaster.c jcomapi.c jcparam.c jcprepct.c jcsample.c jctrans.c 
    jdapimin.c jdapistd.c jdarith.c jdatadst.c jdatasrc.c 
    jdcoefct.c jdcolor.c jddctmgr.c jdhuff.c jdinput.c jdmainct.c 
    jdmarker.c jdmaster.c jdmerge.c jdpostct.c jdsample.c jdtrans.c 
    jerror.c jfdctflt.c jfdctfst.c jfdctint.c jidctflt.c jidctfst.c 
    jidctint.c jmemmgr.c 
    jmemnobs.c jquant1.c jquant2.c jutils.c 
    transupp.c
    jconfig.h 
    jdct.h jerror.h jinclude.h jmemsys.h jmorecfg.h jpegint.h 
    jpeglib.h jversion.h 
    transupp.h
)

if(FREEIMAGE_BUILD_JPEG_STATIC)
  add_library ( LibJPEG_s STATIC ${LIBJPEG_SOURCES} )

  if(FREEIMAGE_BUILD_STATIC)
    install(TARGETS 
    LibJPEG_s
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
    )
    install(FILES jconfig.h jerror.h jmorecfg.h jpegint.h jpeglib.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/LibJPEG")

  endif()

endif(FREEIMAGE_BUILD_JPEG_STATIC)

if(FREEIMAGE_BUILD_JPEG_DLL)
  add_definitions( -DLIBJPEG_BUILD_DLL )
  add_library ( FreeImageJPEG SHARED ${LIBJPEG_SOURCES} )

  install(TARGETS 
    FreeImageJPEG
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
  )
  install(FILES jconfig.h jerror.h jmorecfg.h jpegint.h jpeglib.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/LibJPEG")

endif(FREEIMAGE_BUILD_JPEG_DLL)
