cmake_minimum_required(VERSION 3.22)

project(twgsl)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS OFF)
string(REGEX REPLACE "([\\/\\-]O)3" "\\1z" CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE}")

add_subdirectory(Dependencies)

string(TOUPPER "${CMAKE_BUILD_TYPE}" build_type)

target_compile_options(tint_utils_system PRIVATE "-Wno-disabled-macro-expansion")

add_subdirectory(Core)
