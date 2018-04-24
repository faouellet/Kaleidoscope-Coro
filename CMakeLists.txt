cmake_minimum_required(VERSION 3.10)
project(Kaleidoscope-Coro LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

find_package(LLVM REQUIRED CONFIG)

message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")

include_directories(${LLVM_INCLUDE_DIRS})
add_definitions(${LLVM_DEFINITIONS})

add_executable(kcoro toy.cpp)

llvm_map_components_to_libnames(llvm_libs core orcjit x86asmparser x86codegen)

target_link_libraries(kcoro ${llvm_libs})
