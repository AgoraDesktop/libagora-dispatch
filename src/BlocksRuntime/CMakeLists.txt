
add_library(BlocksRuntime
  data.c
  runtime.c)
if(WIN32)
  target_sources(BlocksRuntime PRIVATE
    BlocksRuntime.def)

  if(NOT BUILD_SHARED_LIBS)
    target_compile_definitions(BlocksRuntime PUBLIC
      BlocksRuntime_STATIC)
    target_compile_options(BlocksRuntime PUBLIC
      "$<$<COMPILE_LANGUAGE:C,CXX>:SHELL:$<$<BOOL:${MSVC}>:-Xclang >-static-libclosure>")
  endif()
endif()

target_include_directories(BlocksRuntime PUBLIC
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
  "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>")
if(HAVE_OBJC AND CMAKE_DL_LIBS)
  target_link_libraries(BlocksRuntime PUBLIC
    ${CMAKE_DL_LIBS})
endif()

if(LINKER_SUPPORTS_BUILD_ID)
  target_link_options(BlocksRuntime PRIVATE "LINKER:--build-id=sha1")
endif()

add_library(BlocksRuntime::BlocksRuntime ALIAS BlocksRuntime)

if(DISPATCH_INSTALL_BLOCK_HEADERS)
  install(FILES Block.h
          DESTINATION ${INSTALL_BLOCK_HEADERS_DIR})
  if(INSTALL_PRIVATE_HEADERS)
    install(FILES Block_private.h
            DESTINATION ${INSTALL_BLOCK_HEADERS_DIR})
  endif()
endif()
set_property(GLOBAL APPEND PROPERTY DISPATCH_EXPORTS BlocksRuntime)
install(TARGETS BlocksRuntime
        EXPORT dispatchExports
        ARCHIVE DESTINATION ${INSTALL_TARGET_DIR}
        LIBRARY DESTINATION ${INSTALL_TARGET_DIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})
