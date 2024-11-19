cmake_minimum_required(VERSION 3.11)
project(
    raylib-tileson
    VERSION 4.2.1
    DESCRIPTION "raylib-tileson"
    HOMEPAGE_URL "https://github.com/VoidMaster23/raylib-tileson.git"
    LANGUAGES CXX
)

# C++17
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Register the cmake folder for find_package()
LIST(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

# raylib-tileson
add_subdirectory(src)

# Examples
option(BUILD_RAYLIB_TILESON_EXAMPLE "Example" ON)
if(BUILD_RAYLIB_TILESON_EXAMPLE)
    add_subdirectory(example)
endif()

# Testing
include(CTest)
enable_testing()
if(BUILD_TESTING)
    set(CTEST_CUSTOM_TESTS_IGNORE
        pkg-config--static
    )
    add_subdirectory(test)
endif()
