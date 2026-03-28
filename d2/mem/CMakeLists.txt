add_library(d2x-mem STATIC
    mem.c
    )

include_directories(../include ../arch/include ../main)

find_package(SDL)
find_package(PhysFS)
target_include_directories(d2x-mem PUBLIC ${SDL_INCLUDE_DIR} ${PHYSFS_INCLUDE_DIR})
