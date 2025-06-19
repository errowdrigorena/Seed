cmake_minimum_required(VERSION 3.26)

# Forzar Clang 16 como compilador predeterminado
set(CMAKE_C_COMPILER   "/usr/bin/clang-16" CACHE FILEPATH "Clang 16 C compiler" FORCE)
set(CMAKE_CXX_COMPILER "/usr/bin/clang++-16" CACHE FILEPATH "Clang 16 C++ compiler" FORCE)

project(crud_server LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Usar libc++ como STL para Clang
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++ -fmodules-ts")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -stdlib=libc++ -fmodules-ts")

# Solo compilar si el generador es Ninja y el compilador es Clang
if (CMAKE_GENERATOR STREQUAL "Ninja" AND CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    add_compile_options(-fmodules-ts)
    add_link_options(-fmodules-ts)
else()
    message(FATAL_ERROR "Este proyecto solo puede compilarse con Ninja y Clang (con soporte de módulos).")
endif()

cmake_policy(SET CMP0155 NEW)

add_executable(crud_server main.cpp hello.cppm)
