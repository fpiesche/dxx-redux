cmake_minimum_required (VERSION 3.21)
project(
    dxx-redux
    VERSION 1.1
    LANGUAGES C CXX
    )

set(LINUX_PKG_PATH "${CMAKE_CURRENT_SOURCE_DIR}/contrib/packaging/linux")

option(D1X "Build D1X-Redux" ON)
option(D2X "Build D2X-Redux" ON)

if(D1X)
  add_subdirectory(d1)
endif()
if(D2X)
  add_subdirectory(d2)
endif()

# Installation
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

# Packaging
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/COPYING.txt")
set(CPACK_RESOURCE_FILE_README "${CMAKE_CURRENT_SOURCE_DIR}/README.md")
set(CPACK_PACKAGE_VERSION_MAJOR ${PROJECT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR ${PROJECT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH ${PROJECT_VERSION_PATCH})
set(CPACK_PACKAGE_CONTACT "https://github.com/dxx-redux/dxx-redux/")
set(CPACK_BUILD_SOURCE_DIRS ${CMAKE_CURRENT_SOURCE_DIR})

set(CPACK_PACKAGE_EXECUTABLES
    "d1x-redux" "D1X-Redux"
    "d2x-redux" "D2X-Redux"
  )
set(CPACK_PACKAGE_ICON ${FREEDESKTOP_APP_ID_DXXR}.svg)

set(CPACK_APPIMAGE_DESKTOP_FILE ${FREEDESKTOP_APP_ID_DXXR}.desktop)

set(CPACK_DEB_COMPONENT_INSTALL ON)
set(CPACK_DEBIAN_FILE_NAME DEB-DEFAULT)
set(CPACK_DEBIAN_DEBUGINFO_PACKAGE ON)
set(CPACK_DEBIAN_PACKAGE_DEPENDS "libsdl1.2debian, libsdl-mixer1.2, libphysfs1, glew, mesa")
set(CPACK_DEBIAN_PACKAGE_HOMEPAGE "https://www.dxx-redux.com/")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "DXX-Redux Contributors")

set(CPACK_RPM_PACKAGE_REQUIRES "sdl12-compat, SDL_mixer, physfs, glew, mesa")
set(CPACK_RPM_PACKAGE_DEBUG ON)

set(CPACK_SOURCE_GENERATOR "TGZ;ZIP")
set(CPACK_SOURCE_IGNORE_FILES
    /.git
    /dist
    /.*build.*
    /\\\\.DS_Store
)
include(CPack)
