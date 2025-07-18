cmake_minimum_required(VERSION 3.23)

project(sdl3_imgui_starter LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)

# Fetch SDL3
message(STATUS "Fetching SDL3 from GitHub")
FetchContent_Declare(
    SDL3
    GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
    GIT_TAG release-3.2.18  # Latest stable SDL3 release as of July 2025; check https://github.com/libsdl-org/SDL/releases for updates
    GIT_SHALLOW TRUE       # Shallow clone for faster download
    GIT_PROGRESS TRUE      # Show progress
)
FetchContent_MakeAvailable(SDL3)

# Fetch Dear ImGui
FetchContent_Declare(
    imgui
    GIT_REPOSITORY https://github.com/ocornut/imgui.git
    GIT_TAG docking
)
# We'll include the ImGui source files directly in our project
FetchContent_MakeAvailable(imgui)

add_library(imgui STATIC 
    ${imgui_SOURCE_DIR}/imgui.cpp
    ${imgui_SOURCE_DIR}/imgui_draw.cpp
    ${imgui_SOURCE_DIR}/imgui_widgets.cpp
    ${imgui_SOURCE_DIR}/imgui_tables.cpp
    ${imgui_SOURCE_DIR}/imgui_demo.cpp

    # SDL3 backend files
    ${imgui_SOURCE_DIR}/backends/imgui_impl_sdl3.cpp
    ${imgui_SOURCE_DIR}/backends/imgui_impl_sdlrenderer3.cpp
)

target_include_directories(imgui PUBLIC ${imgui_SOURCE_DIR} ${imgui_SOURCE_DIR}/backends)
target_link_libraries(imgui PUBLIC SDL3::SDL3)

add_executable(sdl3_imgui_starter main.cpp)
target_link_libraries(sdl3_imgui_starter PRIVATE SDL3::SDL3 imgui)

add_custom_command(TARGET sdl3_imgui_starter POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        $<TARGET_FILE:SDL3::SDL3>
        $<TARGET_FILE_DIR:sdl3_imgui_starter>
)
