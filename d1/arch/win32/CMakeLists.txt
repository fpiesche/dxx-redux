add_library(d1x-arch_win32 STATIC
    crashdump.c
    messagebox.c
    )

include_directories(${CMAKE_SOURCE_DIR}/include ${CMAKE_SOURCE_DIR}/arch/include ${CMAKE_SOURCE_DIR}/main)

target_include_directories(d1x-arch_win32 PUBLIC ${SDL_INCLUDE_DIR})
