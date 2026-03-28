add_library(d2x-arch_x11 STATIC
    messagebox.c
    x11messagebox.c
    )

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/../../include
    ${CMAKE_CURRENT_SOURCE_DIR}/../include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../main
)

target_include_directories(d2x-arch_x11 PUBLIC ${SDL_INCLUDE_DIR})
