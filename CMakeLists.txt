cmake_minimum_required(VERSION 3.10)

# set the project name and version
project("Massdrop Loader" VERSION 1.7)

configure_file(config.h.in config.h)
include_directories("${PROJECT_BINARY_DIR}")

SET(SOURCES
    mdloader_common.c
    mdloader_parser.c
)

if (WIN32) 
SET(SOURCES ${SOURCES} 
    mdloader_win32.c
)
else()
SET(SOURCES ${SOURCES} 
    mdloader_unix.c
)
endif()

if (MSVC) 
SET(SOURCES ${SOURCES} 
    getopt/getopt.c
)
include_directories("getopt/")
endif()

add_executable(mdloader ${SOURCES})
