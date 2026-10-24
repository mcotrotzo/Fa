cmake_minimum_required(VERSION 3.10)
set(VCPKG_TARGET_TRIPLET "x64-mingw-static")
set(VCPKG_HOST_TRIPLET "x64-mingw-static")
set(CMAKE_TOOLCHAIN_FILE "${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake")
project(game)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
find_package(GTest REQUIRED)
find_package(SFML COMPONENTS Network Graphics Window Audio System CONFIG REQUIRED)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
add_executable(game src/main/main.cpp)
target_link_libraries(game PUBLIC SFML::Graphics SFML::Window SFML::System)






enable_testing()
find_package(GTest CONFIG REQUIRED)

add_executable(game-tests src/test/Test.cpp)
target_link_libraries(game-tests PRIVATE GTest::gtest_main)

include(GoogleTest)
gtest_discover_tests(game-tests)
