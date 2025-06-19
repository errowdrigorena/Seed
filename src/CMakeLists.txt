cmake_minimum_required(VERSION 3.29)

project(crud_server LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Forzar Clang 18 y libc++
set(CMAKE_CXX_COMPILER "/usr/bin/clang++-18")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")

# Definir fuentes
set(SRC_MAIN main.cpp)
set(SRC_MODULE hello.ixx)

add_executable(crud_server ${SRC_MAIN})

# Añadir el módulo como FILE_SET (CMake 3.29+)
target_sources(crud_server
    PRIVATE
    FILE_SET cxx_modules TYPE CXX_MODULES FILES ${SRC_MODULE}
)

target_compile_options(crud_server PRIVATE -stdlib=libc++)
target_link_options(crud_server PRIVATE -stdlib=libc++)
