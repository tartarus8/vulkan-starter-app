# Vulkan Starter App

A C++20 Vulkan application that opens a GLFW window and renders the Dear ImGui demo. CMake downloads GLFW, vk-bootstrap, Vulkan Memory Allocator, and ImGui on the first configure, so that step needs an Internet connection.

## macOS

**The app now runs on macOS.** It was verified on an Apple M1 with macOS 15.6.1, Vulkan SDK 1.4.363.0, and MoltenVK. Other Mac configurations have not been tested here.

Install CMake, the Apple command-line developer tools, and the Vulkan SDK. From the repository root, source the SDK environment and build:

```zsh
source "$HOME/VulkanSDK/1.4.363.0/setup-env.sh" # adjust to your SDK version/path
cmake --preset macos-debug
cmake --build build-macos-debug --parallel
./build-macos-debug/vulkan-starter-app
```

`macos-debug` uses Unix Makefiles; Ninja is not needed. For a release build, use `macos-release` and `build-macos-release` in the commands above.

In VS Code, open this folder and run the same commands in its integrated terminal. If you use CMake Tools, select the `macos-debug` configure preset and ensure VS Code has the SDK environment.

## Linux and Windows

A C++20 compiler, CMake, the Vulkan SDK, and the selected CMake generator are required. `debug` and `release` use Ninja; `msvc-debug` and `msvc-release` use Visual Studio 2022; `mingw-debug` and `mingw-release` use MinGW Makefiles.

Configure with the preset for your toolchain, then build its `build-debug` or `build-release` directory. For example, on Linux:

```sh
cmake --preset debug
cmake --build build-debug --parallel
./build-debug/vulkan-starter-app
```

Use a fresh build directory when switching generators. Run the executable from the repository root so relative resource paths resolve correctly.

## Shaders

The current demo does not need external shaders. To add GLSL shaders, add `compile_shader(...)` calls in `CMakeLists.txt` for files under `shaders/`. When `glslc` is available, CMake compiles those files to `.spv` during the build.
