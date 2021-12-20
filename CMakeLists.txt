cmake_minimum_required(VERSION 3.18)
set(PROJECT_NAME GPUOPT)
PROJECT(${PROJECT_NAME} CXX CUDA)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)
# directly make an error if in-source build
if("${PROJECT_SOURCE_DIR}" STREQUAL "${PROJECT_BINARY_DIR}")
    message(FATAL_ERROR "In-source builds are not allowed.\n")
endif()
# Set the RPATH config
# --------------------
# use, i.e. don't skip the full RPATH for the build tree
set(CMAKE_SKIP_BUILD_RPATH  FALSE)
# when building, use the install RPATH already
# (automated test will need this)
set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
# the RPATH to be used when installing
set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")

include(cmake/util.cmake)

set(CUDAToolkit_ROOT $ENV{CUDAToolkit_ROOT})

find_package(CUDAToolkit 11.0 REQUIRED)
set(CMAKE_CUDA_ARCHITECTURES 60 70 80)
OutputCUDAinfo()
add_subdirectory(reduce)

add_subdirectory(GEMM)
