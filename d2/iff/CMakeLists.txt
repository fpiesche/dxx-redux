add_library(d2x-iff STATIC
    iff.c
    )

include_directories(../include ../arch/include ../main)

find_package(SDL)
find_package(PhysFS)
target_include_directories(d2x-iff PUBLIC ${SDL_INCLUDE_DIR} ${PHYSFS_INCLUDE_DIR})
