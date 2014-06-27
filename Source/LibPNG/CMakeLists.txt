cmake_minimum_required(VERSION 2.6.1)

include_directories(${ZLIB_INCLUDE_DIR})

set( LIBPNG_SOURCES 
    png.c
    pngerror.c pngget.c pngmem.c 
    pngpread.c pngread.c pngrio.c pngrtran.c 
    pngrutil.c pngset.c pngtest.c pngtrans.c
    pngwio.c pngwrite.c pngwtran.c pngwutil.c png.h pnglibconf.h pngconf.h 
    pngdebug.h pnginfo.h pngpriv.h pngstruct.h    
)

if(FREEIMAGE_BUILD_PNG_STATIC)
  add_definitions(-D_CRT_SECURE_NO_WARNINGS)

  add_library ( LibPNG_s STATIC ${LIBPNG_SOURCES} )

  if(FREEIMAGE_BUILD_STATIC)
    install(TARGETS 
    LibPNG_s
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
    )
    install(FILES png.h pngconf.h pnglibconf.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/LibPNG")
  endif()

endif(FREEIMAGE_BUILD_PNG_STATIC)

if(FREEIMAGE_BUILD_PNG_DLL)
  set( LIBPNG_DLL_SOURCES 
    ${LIBPNG_SOURCES}
  )

  add_definitions(-DPNG_BUILD_DLL -DZLIB_DLL -D_CRT_SECURE_NO_WARNINGS)

  add_library ( FreeImagePNG SHARED ${LIBPNG_DLL_SOURCES} )
  target_link_libraries( FreeImagePNG FreeImageZlib )

  install(TARGETS 
    FreeImagePNG
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
  )
  install(FILES png.h pngconf.h pnglibconf.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/LibPNG")
endif(FREEIMAGE_BUILD_PNG_DLL)
