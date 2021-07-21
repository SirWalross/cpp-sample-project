cmake_minimum_required(VERSION 3.14)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_CLANG_TIDY "clang-tidy;-checks=*")

project(main)

add_executable(main main.cpp)

find_package(fmt REQUIRED)

target_link_libraries(main PRIVATE fmt::fmt)

add_executable(test-file test.cpp)
set_target_properties(
    test-file
    PROPERTIES
         CXX_CLANG_TIDY ""
)

find_package(GTest CONFIG REQUIRED)

target_link_libraries(test-file PRIVATE GTest::gtest GTest::gtest_main GTest::gmock GTest::gmock_main)
add_test(TESTS test-file)

enable_testing()