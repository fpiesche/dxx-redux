add_library(d1x-misc STATIC
    args.c
    error.c
    hash.c
    hmp.c
    ignorecase.c
    physfsx.c
    strio.c
    strutil.c
    )

if(PNG)
    target_sources(d1x-misc PRIVATE pngfile.c)
endif()

include_directories(../include ../arch/include ../main)

find_package(SDL REQUIRED)
find_package(PhysFS REQUIRED)
find_package(PNG REQUIRED)
target_include_directories(d1x-misc PUBLIC ${SDL_INCLUDE_DIR} ${PHYSFS_INCLUDE_DIR})
