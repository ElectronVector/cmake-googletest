cmake_minimum_required(VERSION 3.25)
project(c_test_exercises C CXX)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)
FetchContent_Declare(
        googletest
        URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

enable_testing()

file(GLOB TEST_SOURCES test/*)
file(GLOB SOURCES src/*)

add_executable(
        c_test_exercises_test
        ${SOURCES}
        ${TEST_SOURCES})
target_link_libraries(
        c_test_exercises_test
        GTest::gtest_main
)
target_include_directories(c_test_exercises_test PRIVATE src/ test/)

include(GoogleTest)
gtest_discover_tests(c_test_exercises_test)

add_executable(c_test_exercises main.c)
