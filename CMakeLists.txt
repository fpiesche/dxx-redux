cmake_minimum_required (VERSION 3.21)
project(
    dxx-redux
    VERSION 1.1
    LANGUAGES C CXX
    )

option(D1X "Build D1X-Redux" ON)
option(D2X "Build D2X-Redux" ON)

if(D1X)
  add_subdirectory(d1)
endif()
if(D2X)
  add_subdirectory(d2)
endif()

if(D1X AND D2X)
  set(FREEDESKTOP_APP_ID_DXXR "com.dxx_redux.dxx-redux")
  if(UNIX AND NOT APPLE)
      install(FILES ${CMAKE_SOURCE_DIR}/contrib/packaging/linux/${FREEDESKTOP_APP_ID_DXXR}.sh
              DESTINATION bin/
              PERMISSIONS WORLD_READ WORLD_EXECUTE
                          GROUP_READ GROUP_EXECUTE
                          OWNER_READ OWNER_WRITE OWNER_EXECUTE)
      install(FILES ${CMAKE_SOURCE_DIR}/contrib/packaging/linux/${FREEDESKTOP_APP_ID_DXXR}.svg
              DESTINATION share/icons/hicolor/scalable/apps/
              PERMISSIONS WORLD_READ WORLD_EXECUTE
                          GROUP_READ GROUP_EXECUTE
                          OWNER_READ OWNER_WRITE OWNER_EXECUTE)
      install(FILES ${CMAKE_SOURCE_DIR}/contrib/packaging/linux/${FREEDESKTOP_APP_ID_DXXR}.png
              DESTINATION share/icons/hicolor/256x256/apps/
              PERMISSIONS WORLD_READ WORLD_EXECUTE
                          GROUP_READ GROUP_EXECUTE
                          OWNER_READ OWNER_WRITE OWNER_EXECUTE)
      install(FILES ${CMAKE_SOURCE_DIR}/contrib/packaging/linux/${FREEDESKTOP_APP_ID_DXXR}.xpm
              DESTINATION share/pixmaps/
              PERMISSIONS WORLD_READ WORLD_EXECUTE
                          GROUP_READ GROUP_EXECUTE
                          OWNER_READ OWNER_WRITE OWNER_EXECUTE)
      install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/contrib/packaging/linux/${FREEDESKTOP_APP_ID_DXXR}.metainfo.xml
              DESTINATION share/metainfo/
              PERMISSIONS WORLD_READ WORLD_EXECUTE
                          GROUP_READ GROUP_EXECUTE
                          OWNER_READ OWNER_WRITE OWNER_EXECUTE)
      install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/contrib/packaging/linux/${FREEDESKTOP_APP_ID_DXXR}.desktop
              DESTINATION share/applications/
              PERMISSIONS WORLD_READ WORLD_EXECUTE
                          GROUP_READ GROUP_EXECUTE
                          OWNER_READ OWNER_WRITE OWNER_EXECUTE)
  endif()
endif()
