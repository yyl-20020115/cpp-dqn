file(GLOB SOURCES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
  ./*.cpp
  ./models/*.cpp
  ./controllers/*.cpp
  ./explorations/*.cpp)

add_library(dqn SHARED ${SOURCES})

target_include_directories(dqn PUBLIC ${PROJECT_SOURCE_DIR}/third_party/Arcade-Learning-Environment-master/src)
target_include_directories(dqn PUBLIC ${PROJECT_SOURCE_DIR}/include)
target_include_directories(dqn PUBLIC /usr/local/include)

# SDL
if (USE_SDL)
  find_library(SDL_LIBRARY SDL HINTS /usr/local/lib)
  target_link_libraries(dqn PUBLIC ${SDL_LIBRARY})
  find_library(SDL_GFX_LIBRARY SDL_gfx HINTS /usr/local/lib)
  target_link_libraries(dqn PUBLIC ${SDL_GFX_LIBRARY})
  find_library(SDL_IMAGE_LIBRARY SDL_image HINTS /usr/local/lib)
  target_link_libraries(dqn PUBLIC ${SDL_IMAGE_LIBRARY})
  find_library(SDL_MAIN_LIBRARY SDLmain HINTS /usr/local/lib)
  target_link_libraries(dqn PUBLIC ${SDL_MAIN_LIBRARY})
endif()

# ALE
#target_link_libraries(dqn PUBLIC ${PROJECT_SOURCE_DIR}/third_party/Arcade-Learning-Environment-master/libale.so)
target_link_libraries(dqn PUBLIC ${PROJECT_SOURCE_DIR}/third_party/Arcade-Learning-Environment-master/build/src/Debug/ale.lib)

# NNabla
target_include_directories(dqn PUBLIC ${NNABLA_INCLUDE_DIRS} ${pybind11_INCLUDE_DIRS})
message(STATUS "Pybind11 include dirs: ${pybind11_INCLUDE_DIRS}")
message(STATUS "NNabla library: ${NNABLA_LIBRARY}")
message(STATUS "NNabla utils library: ${NNABLA_UTILS_LIBRARY}")
message(STATUS "NNabla include dirs: ${NNABLA_INCLUDE_DIRS}")

target_link_libraries(dqn PUBLIC ${NNABLA_LIBRARY} ${NNABLA_UTILS_LIBRARY})

# NNabla CUDA extension
if (GPU)
  find_library(NNABLA_CUDA_LIBRARY nnabla_cuda HINTS /usr/local/lib)
  target_link_libraries(dqn PUBLIC ${NNABLA_CUDA_LIBRARY})
endif()
