cmake_minimum_required(VERSION 2.6.1)

include_directories(${ZLIB_INCLUDE_DIR})

set( LIBTIFF_SOURCES 
tif_aux.c 
tif_close.c tif_codec.c tif_color.c tif_compress.c 
tif_dir.c tif_dirinfo.c tif_dirread.c tif_dirwrite.c 
tif_dumpmode.c tif_error.c tif_extension.c tif_fax3.c 
tif_fax3sm.c tif_flush.c tif_getimage.c tif_jbig.c tif_jpeg.c 
tif_luv.c tif_lzw.c tif_next.c tif_ojpeg.c tif_open.c 
tif_packbits.c tif_pixarlog.c tif_predict.c tif_print.c tif_read.c 
tif_strip.c tif_swab.c tif_thunder.c tif_tile.c tif_version.c 
tif_warning.c tif_write.c tif_zip.c 
tif_stream.cxx t4.h tif_config.h tif_config.vc.h tif_dir.h 
tif_fax3.h tif_predict.h tiff.h 
)

if(FREEIMAGE_BUILD_TIFF_STATIC)
  add_library(LibTIFF_s ${LIBTIFF_SOURCES})

  if(FREEIMAGE_BUILD_STATIC)
    install(TARGETS 
    LibTIFF_s
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
    )
    install(FILES tiff.h tiffconf.h tiffio.h tiffvers.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/LibTIFF")
  endif()
endif(FREEIMAGE_BUILD_TIFF_STATIC)

if(FREEIMAGE_BUILD_TIFF_DLL)

  set( LIBTIFF_DLL_SOURCES 
    ${LIBTIFF_SOURCES}
    tif_win32.c
    libtiff.def
  )

  add_definitions(-DTIF_PLATFORM_CONSOLE)

  add_library ( FreeImageTIFF SHARED ${LIBTIFF_DLL_SOURCES} )
  target_link_libraries( FreeImageTIFF FreeImageJPEG )
  target_link_libraries( FreeImageTIFF FreeImageZlib )

  install(TARGETS 
    FreeImageTIFF
    RUNTIME DESTINATION "${CMAKE_INSTALL_PREFIX}/bin" 
    ARCHIVE DESTINATION "${CMAKE_INSTALL_PREFIX}/lib" 
    LIBRARY DESTINATION "${CMAKE_INSTALL_PREFIX}/lib"
  )
  install(FILES tiff.h tiffconf.h tiffio.h tiffvers.h DESTINATION "${CMAKE_INSTALL_PREFIX}/include/LibTIFF")

endif(FREEIMAGE_BUILD_TIFF_DLL)
