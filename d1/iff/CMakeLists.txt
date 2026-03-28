add_library(d1x-iff STATIC
    iff.c
    )

include_directories(../include ../arch/include ../main)

find_package(SDL)
find_package(PhysFS)
target_include_directories(d1x-iff PUBLIC ${SDL_INCLUDE_DIR} ${PHYSFS_INCLUDE_DIR})
