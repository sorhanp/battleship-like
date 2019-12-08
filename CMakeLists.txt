cmake_minimum_required(VERSION 3.1)
set(CMAKE_C_STANDARD 11)
project(battleships-like    VERSION 0.1.0
                            DESCRIPTION "Battleships like game made in C and SDL"
                            LANGUAGES C)

set(BUILD_TESTING false)

if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    # See if SDL2 is installed
    find_package(SDL2 REQUIRED)
    if(SDL2_FOUND)
        message(STATUS "SDL2_INCLUDE_DIRS: ${SDL2_INCLUDE_DIRS}")
        include_directories(${SDL2_INCLUDE_DIRS})
        # Compile options for SDL
        add_compile_options(-lSDL2main -lSDL2)
    endif()

    # Docs only available if this is the main app
    find_package(Doxygen)
        if(Doxygen_FOUND)
            add_subdirectory(docs)
        else()
            message(STATUS "Doxygen not found, not building docs")
        endif()

    include(CTest)
endif()

# Include sources
add_subdirectory(src)
 
if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME AND BUILD_TESTING)
    add_subdirectory(tests)
endif()