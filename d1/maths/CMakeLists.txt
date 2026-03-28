add_library(d1x-maths STATIC
    fixc.c
    rand.c
    tables.c
    vecmat.c
    )

include_directories(../include ../arch/include ../main)

find_package(SDL)
target_include_directories(d1x-maths PUBLIC ${SDL_INCLUDE_DIR})
