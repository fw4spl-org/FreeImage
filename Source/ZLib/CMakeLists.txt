
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

if(FREEIMAGE_BUILD_ZLIB_STATIC)
  add_library (Zlib_s STATIC ${ZLIB_SOURCES} )

  if(FREEIMAGE_BUILD_STATIC)
    install(TARGETS 
    Zlib_s
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
    )
    install(FILES zlib.h zconf.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/zlib")
  endif()  

endif(FREEIMAGE_BUILD_ZLIB_STATIC)

if(FREEIMAGE_BUILD_ZLIB_DLL)

  add_definitions(-DZLIB_DLL)
  set( ZLIB_SOURCES_DLL
    ${ZLIB_SOURCES}
  )

  add_library (FreeImageZlib SHARED ${ZLIB_SOURCES_DLL} )

  install(TARGETS 
    FreeImageZlib
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
  )
  install(FILES zlib.h zconf.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/Zlib")

endif(FREEIMAGE_BUILD_ZLIB_DLL)
