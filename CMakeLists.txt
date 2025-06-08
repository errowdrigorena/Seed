cmake_minimum_required(VERSION 3.26)
project(crud_server LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include(FetchContent)

add_subdirectory(src)
# add_subdirectory(tests)
# add_subdirectory(bench)
