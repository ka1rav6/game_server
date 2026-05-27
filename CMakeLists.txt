cmake_minimum_required(VERSION 3.16)

project(game_server LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Threads REQUIRED)

add_definitions(-DASIO_STANDALONE)

set(CORE_SRCS
    src/Player.cpp
    src/Point.cpp
    src/gameState.cpp
)

add_library(game_core STATIC ${CORE_SRCS})
target_include_directories(game_core PUBLIC include)

add_executable(server src/server_main.cpp)
target_link_libraries(server PRIVATE game_core Threads::Threads)

add_executable(client src/client_main.cpp)
target_link_libraries(client PRIVATE game_core Threads::Threads)