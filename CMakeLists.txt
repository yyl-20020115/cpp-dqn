cmake_minimum_required(VERSION 3.24)
enable_language(CXX)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED OFF)
set(CMAKE_CXX_EXTENSIONS ON)
project(dqn CXX)

option(USE_SDL "Use SDL for ALE" ON)
option(DEBUG "Enable debug option" OFF)
option(GPU "Enable gpu" OFF)

if (DEBUG)
  set(COMPILE_OPTION "-g -O0")
else()
  set(COMPILE_OPTION "-O3")
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall ${COMPILE_OPTION}")

find_library(pybind11 CONFIG)
find_library(NNABLA_LIBRARY nnabla HINTS /usr/local/lib)
find_library(NNABLA_UTILS_LIBRARY nnabla_utils HINTS /usr/local/lib)
find_library(NNABLA_INCLUDE_DIRS nnabla HINTS /usr/local/include)


add_subdirectory(third_party)
add_subdirectory(src/dqn)
add_subdirectory(tests)
add_subdirectory(examples)
