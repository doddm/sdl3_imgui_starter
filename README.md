# sdl3_imgui_starter

A minimal C++ starter project for SDL3 and Dear ImGui, managed with CMake.

This project demonstrates how to set up a basic SDL3 window and render an ImGui debug window. CMake automatically fetches SDL3 and ImGui as dependencies and builds SDL3.

## Features

- **Single-file**: All logic is in `main.cpp`.
- **No manual dependency setup**: CMake's FetchContent downloads and builds SDL3 and ImGui for you.
- **Cross-platform ready**: Should work on Windows, Linux, and macOS (tested on Windows).
- **No vendor blobs**: No third-party source code checked in.

## Requirements

- [CMake](https://cmake.org/) 3.23 or newer
- A C++17-compatible compiler (e.g. MSVC 2022, GCC 11+, Clang 13+)
- Internet connection (for first build, to fetch dependencies)

## Building

```sh
git clone https://github.com/doddm/sdl3_imgui_starter.git
cd sdl3_imgui_starter
cmake -B cmake_build
cmake --build cmake_build