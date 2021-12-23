cmake_minimum_required(VERSION 3.0)

# Create project
set(ProjectName "main")
project(${ProjectName})

# Compile option
if(NOT MSVC)
    set(CMAKE_C_FLAGS "-Wall")
    set(CMAKE_C_FLAGS_RELEASE "-O2 -DNDEBUG")
    set(CMAKE_C_FLAGS_DEBUG "-g3 -O0")
    set(CMAKE_CXX_FLAGS "${CMAKE_C_FLAGS} -std=c++11 -lstdc++")
    set(CMAKE_CXX_FLAGS_RELEASE ${CMAKE_C_FLAGS_RELEASE})
    set(CMAKE_CXX_FLAGS_DEBUG ${CMAKE_C_FLAGS_DEBUG})
    if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
        message(STATUS "No build type selected, default to Release")
        set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Build type (default Debug)" FORCE)
    endif()
endif()

# Create executable file
add_executable(${ProjectName}
    main.cpp
)

# For OpenGL
find_package(OpenGL REQUIRED)
target_link_libraries(${ProjectName} ${OPENGL_gl_LIBRARY} ${OPENGL_glu_LIBRARY})
target_link_libraries(${ProjectName} ${OPENGL_LIBRARIES})
target_include_directories(${ProjectName} PUBLIC ${OPENGL_INCLUDE_DIR})

# For GLFW
set(GLFW_DIR "${CMAKE_CURRENT_LIST_DIR}/../third_party/glfw")
add_subdirectory(${GLFW_DIR} glfw)
target_link_libraries(${ProjectName} glfw ${GLFW_LIBRARIES})
target_include_directories(${ProjectName} PUBLIC ${GLFW_DIR}/include)

# For ImGui (reference: example_glfw_opengl3/Makefile)
set(IMGUI_DIR "${CMAKE_CURRENT_LIST_DIR}/../third_party/imgui")
target_sources(${ProjectName} PRIVATE 
  ${IMGUI_DIR}/imgui.cpp
  ${IMGUI_DIR}/imgui_demo.cpp
  ${IMGUI_DIR}/imgui_draw.cpp
  ${IMGUI_DIR}/imgui_tables.cpp 
  ${IMGUI_DIR}/imgui_widgets.cpp
  ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp
  ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp
)
target_include_directories(${ProjectName} PUBLIC ${IMGUI_DIR} ${IMGUI_DIR}/backends)

# Copy files
# file(COPY ${CMAKE_SOURCE_DIR}/../resource DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
# add_definitions(-DRESOURCE="resource")