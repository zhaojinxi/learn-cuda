cmake_minimum_required(VERSION 3.20)

project(cuda_debug_example VERSION 0.1.0 LANGUAGES CXX CUDA)

set(CMAKE_BUILD_TYPE "Debug")

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_COMPILER "g++")
set(CMAKE_CXX_FLAGS "-Wall")
set(CMAKE_CXX_FLAGS_DEBUG "-O0 -g")
# set(CMAKE_CXX_FLAGS_DEBUG "-O0 -pedantic-errors -Weffc++ -Wextra -Wsign-conversion -Werror -g")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -DNDEBUG")
# set(CMAKE_CXX_COMPILER "clang++")
# set(CMAKE_CXX_FLAGS "-Wall -stdlib=libc++")

set(CMAKE_CUDA_STANDARD 11)
set(CMAKE_CUDA_STANDARD_REQUIRED ON)
set(CMAKE_CUDA_ARCHITECTURES OFF)
set(CMAKE_CUDA_FLAGS "-Wall")
set(CMAKE_CUDA_FLAGS_DEBUG "-O0 -g -G")
set(CMAKE_CUDA_FLAGS_RELEASE "-O3 -DNDEBUG")

find_package(CUDAToolkit REQUIRED)
include_directories(${CUDA_INCLUDE_DIRS})

include_directories(include)
aux_source_directory(src sources)

add_executable(${PROJECT_NAME} ${sources})
target_link_libraries(${PROJECT_NAME} PRIVATE CUDA::cudart)
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES})
