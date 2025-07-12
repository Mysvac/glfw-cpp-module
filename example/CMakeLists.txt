cmake_minimum_required(VERSION 4.0.0)

# set(CMAKE_EXPERIMENTAL_CXX_IMPORT_STD "......")

file(TO_CMAKE_PATH "$ENV{VCPKG_ROOT}" VCPKG_CMAKE_PATH)
set(CMAKE_TOOLCHAIN_FILE "${VCPKG_CMAKE_PATH}/scripts/buildsystems/vcpkg.cmake")

project(HelloGLFW LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_MODULE_STD 1)

include(VulkanHppModule.cmake)

find_package(glfw3 CONFIG REQUIRED)

add_executable(main src/main.cpp)
target_sources(main PRIVATE
    FILE_SET cxx_modules
    TYPE CXX_MODULES
    FILES src/glfw.cppm
)

target_link_libraries(main PRIVATE VulkanHppModule)
target_link_libraries(main PRIVATE glfw )


