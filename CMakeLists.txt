cmake_minimum_required(VERSION 2.8.11)
project(circuit-of-mana-prototype)

find_package(Git)
if(NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/externals/ugdk/CMakeLists.txt")
    if(GIT_FOUND)
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init
                        WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}")
    else(GIT_FOUND)
        message(FATAL_ERROR "Git submodule 'externals/ugdk' not initialized and git not found.")
    endif(GIT_FOUND)
endif()
add_subdirectory(externals/ugdk)

if(CMAKE_COMPILER_IS_GNUCC)
    add_definitions(-std=gnu++0x)
endif()

set(SRCS
    ./src/main.cc
)

add_ugdk_executable(circuit-of-mana ${SRCS})
