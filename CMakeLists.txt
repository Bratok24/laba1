cmake_minimum_required(VERSION 3.15)

set(PATCH_VERSION "1" CACHE STRING "Patch version")
set(PROJECT_VERSION "1.0.${PATCH_VERSION}")

project(HelloApp VERSION ${PROJECT_VERSION} LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Генерируем version.h из шаблона version.h.in
configure_file(version.h.in version.h)

# Библиотека с логикой
add_library(hellolib lib.cpp)
target_include_directories(hellolib PUBLIC "${CMAKE_BINARY_DIR}")

# Основное приложение
add_executable(hello_app main.cpp)
target_link_libraries(hello_app PRIVATE hellolib)

# Тесты через CTest (без Boost)
enable_testing()
add_test(NAME version_test COMMAND hello_app)
set_tests_properties(version_test PROPERTIES
    PASS_REGULAR_EXPRESSION "Hello, World! Version 1.0.${PATCH_VERSION}"
)