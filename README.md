# About
- just a sample project to use ImGui ( https://github.com/ocornut/imgui )

# Note
## Windows 11
- Visual Studio 2019 + cmake-gui

## WSL2 on Windows 11
- `apt install cmake build-essential`
- `apt install libglu1-mesa-dev mesa-common-dev libxrandr-dev libxinerama-dev libxcursor-dev libxi-dev`
- Execution on WSL2 (NVIDIA Drivers for CUDA on WSL is installed) failed in my PC for some reasons... Instead, it works on ubuntu:20.04 docker on WSL2
    - `glfwInit` returned `GL_FALSE`
