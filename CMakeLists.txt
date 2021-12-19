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



function(OutputCUDAinfo)
    message ( STATUS "CUDAToolkit_FOUND = ${CUDAToolkit_FOUND}" )
    message ( STATUS "CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES = ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES}" )
    message ( STATUS "CUDAToolkit_VERSION = ${CUDAToolkit_VERSION}" )
    message ( STATUS "CUDAToolkit_VERSION_MAJOR = ${CUDAToolkit_VERSION_MAJOR}" )
    message ( STATUS "CUDAToolkit_VERSION_MINOR = ${CUDAToolkit_VERSION_MINOR}" )
    message ( STATUS "CUDAToolkit_VERSION_PATCH = ${CUDAToolkit_VERSION_PATCH}" )
    message ( STATUS "CUDAToolkit_BIN_DIR = ${CUDAToolkit_BIN_DIR}" )
    message ( STATUS "CUDAToolkit_INCLUDE_DIRS = ${CUDAToolkit_INCLUDE_DIRS}" )
    message ( STATUS "CUDAToolkit_LIBRARY_DIR = ${CUDAToolkit_LIBRARY_DIR}" )
    message ( STATUS "CUDAToolkit_LIBRARY_ROOT = ${CUDAToolkit_LIBRARY_ROOT}" )
    message ( STATUS "CUDAToolkit_TARGET_DIR = ${CUDAToolkit_TARGET_DIR}" )
    message ( STATUS "CUDAToolkit_NVCC_EXECUTABLE = ${CUDAToolkit_NVCC_EXECUTABLE}" )
    message ( STATUS "CMAKE_CUDA_FLAGS = ${CMAKE_CUDA_FLAGS}" )
    message ( STATUS "CUDA_STANDARD = ${CUDA_STANDARD}" )
    message ( STATUS "CMAKE_CUDA_EXTENSIONS = ${CMAKE_CUDA_EXTENSIONS}" )
endfunction()

set(CUDAToolkit_ROOT $ENV{CUDAToolkit_ROOT})

find_package(CUDAToolkit 11.0 REQUIRED)
set(CMAKE_CUDA_ARCHITECTURES 60 70 80)
OutputCUDAinfo()
add_subdirectory(reduce)

#add_subdirectory(GEMM)
