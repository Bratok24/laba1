cmake_minimum_required(VERSION 3.15)
project(HelloWorld VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(hello main.cpp)
target_compile_definitions(hello PRIVATE PROJECT_VERSION="${PROJECT_VERSION}")

enable_testing()
add_test(NAME hello_test COMMAND hello)
set_tests_properties(hello_test PROPERTIES PASS_REGULAR_EXPRESSION "Hello, World! Version")