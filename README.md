# Raylib CMake Template

This template simplifies the setup process for raylib using CMake FetchContent. It automatically fetches and configures raylib along with a few optional game development libraries. Fast and easy way to start your game dev journey with raylib using this straightforward template.

### libraries supported

- [raylib](https://github.com/raysan5/raylib) - A simple and easy-to-use library to enjoy videogames programming.
- [ImGui](https://github.com/ocornut/imgui) - Dear ImGui: Bloat-free Graphical User interface for C++ with minimal dependencies.
- [LDtkLoader](https://github.com/Madour/LDtkLoader) - Used to load and help
  with drawing a map made with the awesome [LDtk](https://ldtk.io/).
- [box2d](https://github.com/erincatto/box2d) - Ubiquitous and easy to use 2D
  physics engine.
- [fmt](https://github.com/fmtlib/fmt) - Logging and string formatting library
  that makes your life much easier.
- [bullet3](https://github.com/bulletphysics/bullet3) - 3d physics engine.
- [reactphysics3d](https://github.com/DanielChappuis/ReactPhysics3D) - Open source C++ physics engine library in 3D. - Note Wasm not working
- [JoltPhysics](https://github.com/jrouwe/JoltPhysics) - A multi core friendly rigid body physics and collision detection library, written in C++, suitable for games and VR applications.

### How to use this template

#### Prerequisites
- [cmake](https://cmake.org/)
- [mingw](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/seh/) or [Visual Studio](https://visualstudio.microsoft.com/) with [Desktop development with c++](https://learn.microsoft.com/en-us/cpp/build/vscpp-step-0-installation?view=msvc-170)
- [Emscripten](https://github.com/emscripten-core/emsdk) (for web build)


### Choosing What libraries to use
```bash
## In CmakeLists.txt edit the following at the top

## Toggle a library with ON or OFF

option(USE_RAYLIB "Use raylib" ON)
option(USE_MINIMAL_RAYLIB_MODULES "Use minimal raylib modules" OFF)
option(USE_IMGUI "Use ImGui" OFF)
option(USE_NO_ASSETS "Use no assets" OFF)
option(USE_LDTKLOADER "Use LDtk Loader" OFF)
option(USE_FMT "Use fmt" OFF)
option(USE_BOX2D "Use Box2D" OFF)
option(USE_BULLET3 "Use Bullet Physics 3D" OFF)
option(USE_REACTPHYSICS3D "Use React Physics 3D" OFF)
option(USE_JOLTPHYSICS "Use Jolt Physics 3D" OFF)

```

## Building for Desktop

```bash
## supported windows and linux

## Clone the repository
git clone https://github.com/BrettWilsonDev/raylib-cmake.git

## Navigate to the project directory
cd raylib-cmake

## Create a build directory
mkdir build

## Navigate to the build directory
cd build

## Run CMake to configure the project
cmake -DCMAKE_BUILD_TYPE=Release ..

## Build the project
cmake --build . --config Release

## The executable is found in the build directory either in the root of the directory or in debug/release file if using msvc
```

## Building for the Web

```bash
## Ensure Emscripten is installed and configured:
## on windows
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
./emsdk.bat install latest
./emsdk.bat activate latest --permanent

## add emsdk to path ex: C:\Program Files\emsdk

## on linux
cd /usr/local
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
./emsdk install latest
./emsdk activate latest --permanent

## add emsdk to path

## Navigate to the project directory
cd raylib-cmake

## Change to tools dir
cd tools

## Run the build script for the web
.\build_for_web.bat async

## If emscripten_set_main_loop_arg is set up then just use:
.\build_for_web.bat

## This gives much better performance in the web
## Example of how to use emscripten_set_main_loop_arg below

```
##### emscripten_set_main_loop_arg example

```c++
void ClassName::MainLoopHelper(void *userData)
{
    ClassName *className = static_cast<ClassName *>(userData);

    className->Draw(); // call your game functions here
}

// main loop
void ClassName::Run() // Run() is called from a ClassName instance in main
{
#if defined(PLATFORM_WEB)
    emscripten_set_main_loop_arg(MainLoopHelper, this, 0, 1);
#else
    while (!WindowShouldClose())
    {
        MainLoopHelper(this);
    }
#endif

// replace ClassName with the name of your class and function names with your functions
```

### Troubleshooting

```bash
## Linux

## Dont forget to install
build-essential

## If missing package issues arise while trying to build in linux you may need to install or update the following:

libx11-dev
libxrandr-dev
libxinerama-dev
libxcursor-dev
libxi-dev

## If missing opengl. install or update
libgl1-mesa-dev
```

## Acknowledgments

- [raylib-cpp-cmake-template](https://github.com/tupini07/raylib-cpp-cmake-template) - Raylib cmake starting point template by [tupini07](https://github.com/tupini07).
