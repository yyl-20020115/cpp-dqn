
# message(STATUS "NNABLA_INCLUDE_DIR: ${NNABLA_INCLUDE_DIR}")

add_executable(run_game run_game.cpp)
target_link_libraries(run_game dqn)
set_property(TARGET run_game PROPERTY RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/bin")

if(GPU)
  add_definitions(-DGPU)
endif()


include_directories(${PROJECT_BINARY_DIR}/third_party/gflags-2.2.2/include )

add_executable(train train.cpp)
target_link_libraries(train dqn gflags)
target_include_directories(train PRIVATE ${NNABLA_INCLUDE_DIRS})
set_property(TARGET train PROPERTY RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/bin")

add_executable(play play.cpp)
target_link_libraries(play dqn gflags)
set_property(TARGET play PROPERTY RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/bin")
