add_library(d2x-misc STATIC
    args.c
    error.c
    hash.c
    hmp.c
    ignorecase.c
    physfsrwops.c
    physfsx.c
    strio.c
    strutil.c
    )

if(PNG)
    target_sources(d2x-misc PRIVATE pngfile.c)
    find_package(PNG REQUIRED)
    target_include_directories(d2x-misc PUBLIC ${PNG_INCLUDE_DIR})
endif()

include_directories(../include ../arch/include ../main)

find_package(SDL REQUIRED)
find_package(PhysFS REQUIRED)
target_include_directories(d2x-misc PUBLIC ${SDL_INCLUDE_DIR} ${PHYSFS_INCLUDE_DIR})
