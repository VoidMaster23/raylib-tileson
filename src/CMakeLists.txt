# Define options for building static or shared libraries
option(RAYLIB_TILESON "Build raylib-tileson as static library" ON)
option(RAYLIB_TILESON_SHARED "Build raylib-tileson as shared library" OFF)

# Check if the include directory exists
set(TILESON_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../include")

if(NOT EXISTS ${TILESON_INCLUDE_DIR})
    message(FATAL_ERROR "Include directory not found: ${TILESON_INCLUDE_DIR}")
endif()

# Build the static library if RAYLIB_TILESON is ON
if(RAYLIB_TILESON)
    # Prevent redefinition
    if(NOT TARGET raylib-tileson)
        add_library(raylib-tileson STATIC "raylib-tileson.cpp")
        target_include_directories(raylib-tileson PUBLIC ${TILESON_INCLUDE_DIR})
        target_link_libraries(raylib-tileson PUBLIC raylib)
        message(STATUS "Building static library: raylib-tileson")
    endif()
endif()

# Build the shared library if RAYLIB_TILESON_SHARED is ON
if(RAYLIB_TILESON_SHARED)
    # Prevent redefinition
    if(NOT TARGET raylib-tileson-shared)
        add_library(raylib-tileson-shared SHARED "raylib-tileson.cpp")
        target_include_directories(raylib-tileson-shared PUBLIC ${TILESON_INCLUDE_DIR})
        target_link_libraries(raylib-tileson-shared PUBLIC raylib)
        message(STATUS "Building shared library: raylib-tileson-shared")
    endif()
endif()
