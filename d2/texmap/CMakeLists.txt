add_library(d2x-texmap STATIC
    ntmap.c
    scanline.c
    )

include_directories(../include ../arch/include ../main)

if(NOT OPENGL)
    target_sources(d2x-texmap PRIVATE tmapflat.c)
    if(ASM)
        if(NOT CMAKE_ASM_${ASM_DIALECT}_COMPILE_OBJECT)
            set(CMAKE_ASM_${ASM_DIALECT}_COMPILE_OBJECT "<CMAKE_ASM_${ASM_DIALECT}_COMPILER> -o <OBJECT> <SOURCE>")
        endif()
        target_sources(d2x-texmap PRIVATE
            tmap_ll.asm
            tmap_flt.asm
            tmapfade.asm
            tmap_lin.asm
            tmap_per.asm
            )
    else()
        target_compile_definitions(d2x-texmap PUBLIC NO_ASM)
    endif()
else()
    target_compile_definitions(d2x-texmap PUBLIC NO_ASM)
endif()

find_package(SDL)
find_package(PhysFS)
target_include_directories(d2x-texmap PUBLIC ${SDL_INCLUDE_DIR} ${PHYSFS_INCLUDE_DIR})
