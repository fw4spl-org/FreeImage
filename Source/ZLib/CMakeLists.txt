
set( ZLIB_SOURCES
adler32.c
compress.c
crc32.c
deflate.c
infback.c
inffast.c
inflate.c
inftrees.c
trees.c
uncompr.c
zutil.c
crc32.h
deflate.h
inffast.h
inffixed.h
inflate.h
inftrees.h
trees.h
zconf.h
zlib.h
zutil.h
    )

IF(FREEIMAGE_BUILD_ZLIB_STATIC)
  add_library (Zlib_s STATIC ${ZLIB_SOURCES} )

  IF(FREEIMAGE_BUILD_STATIC)
    INSTALL(TARGETS 
    Zlib_s
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
    )
    INSTALL(FILES zlib.h zconf.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/zlib")
  ENDIF()  

ENDIF(FREEIMAGE_BUILD_ZLIB_STATIC)

IF(FREEIMAGE_BUILD_ZLIB_DLL)

  ADD_DEFINITIONS(-DZLIB_DLL)
  set( ZLIB_SOURCES_DLL
    ${ZLIB_SOURCES}
  )

  add_library (FreeImageZlib SHARED ${ZLIB_SOURCES_DLL} )

  INSTALL(TARGETS 
    FreeImageZlib
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
  )
  INSTALL(FILES zlib.h zconf.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/Zlib")

ENDIF(FREEIMAGE_BUILD_ZLIB_DLL)
