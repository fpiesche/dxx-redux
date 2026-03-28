add_library(d1x-arch_sdl STATIC
    event.c
    init.c
    joy.c
    key.c
    mouse.c
    rbaudio.c
    timer.c
    window.c
    digi.c
    digi_audio.c
    )
if(NOT OPENGL)
    target_sources(d1x-arch_sdl PRIVATE gr.c)
endif()
if(SDLMIXER)
    target_sources(d1x-arch_sdl PRIVATE
        digi_mixer.c
        digi_mixer_music.c
        jukebox.c
        )
    target_include_directories(d1x-arch_sdl PUBLIC ${SDL_MIXER_INCLUDE_DIRS})
    target_link_libraries(d1x-arch_sdl ${SDL_MIXER_LIBRARY})
endif()

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/../../include
    ${CMAKE_CURRENT_SOURCE_DIR}/../include
    ${CMAKE_CURRENT_SOURCE_DIR}/../../main
)

target_compile_definitions(d1x-arch_sdl PUBLIC
    DXX_VERSION_MAJORi=${PROJECT_VERSION_MAJOR}
    DXX_VERSION_MINORi=${PROJECT_VERSION_MINOR}
    DXX_VERSION_MICROi=$<IF:$<BOOL:${PROJECT_VERSION_MICRO}>,${PROJECT_VERSION_MICRO},0>
    )

find_package(SDL)
find_package(PhysFS)
target_include_directories(d1x-arch_sdl PUBLIC ${SDL_INCLUDE_DIR} ${PHYSFS_INCLUDE_DIR})
