add_library(d2x-libmve STATIC
    decoder8.c
    decoder16.c
    mve_audio.c
    mvelib.c
    mveplay.c
    )

include_directories(../include ../arch/include ../main)

find_package(SDL)
target_include_directories(d2x-libmve PUBLIC ${SDL_INCLUDE_DIR})

if(SDLMIXER)
    target_link_libraries(d2x-libmve PUBLIC ${SDL_MIXER_LIBRARY})
endif()

include(CheckStructHasMember)
check_struct_has_member("struct timeval" tv_sec sys/time.h HAVE_STRUCT_TIMEVAL LANGUAGE C)
if(HAVE_STRUCT_TIMEVAL)
    target_compile_definitions(d2x-libmve PUBLIC HAVE_STRUCT_TIMEVAL=1)
endif()
check_struct_has_member("struct timespec" tv_sec sys/time.h HAVE_STRUCT_TIMESPEC LANGUAGE C)
if(HAVE_STRUCT_TIMESPEC)
    target_compile_definitions(d2x-libmve PUBLIC HAVE_STRUCT_TIMESPEC=1)
endif()
