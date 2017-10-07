cmake_minimum_required(VERSION 3.1)

# sets the project name to the current homework
get_filename_component(ProjectName ${CMAKE_CURRENT_SOURCE_DIR} NAME)
project(${ProjectName} C CXX)

# Verbose compilation - enable if you need to debug compiler flags #
set(CMAKE_VERBOSE_MAKEFILE OFF)

# any additional packages here #
# find_package(Threads REQUIRED)

# include ParallelUtil #
include(ParallelUtils.cmake)

# require C++14 support #
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# disallow in-source builds
# i.e. require that you be in a "build/" folder such that intermediate
# build files are not in the same area as your source code
if ("${CMAKE_SOURCE_DIR}" STREQUAL "${CMAKE_BINARY_DIR}")
    message(SEND_ERROR "In-source builds are not allowed.")
endif()

# additional compiler-specific options #
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    # using Clang
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    # using GCC
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Wno-missing-field-initializers -Wsign-conversion -Wsign-compare -march=native -pedantic")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wno-missing-field-initializers -Wsign-conversion -Wsign-compare -march=native -pedantic")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Intel")
    # using Intel C++
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
    # using Visual Studio C++
    # Compile with W4 (highest warning level)
    if(CMAKE_CXX_FLAGS MATCHES "/W[0-4]")
        string(REGEX REPLACE "/W[0-4]" "/W4" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
    else()
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
    endif()
endif()

# set include directories here #
include_directories(.)

# set output directory as the same as the HW dir #
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR})

# enable parallel libraries here #
#enable_intel_avx()
#enable_mpi_support()
#enable_openmp_support()
#enable_cuda_support()

# executable setup here #
## Example MPI program
#add_executable(integrate_mpi integrate_mpi.cpp)
#target_link_libraries(integrate_mpi ${MPI_CXX_LIBRARIES})

## Example OpenMP program
#add_executable(integrate_omp integrate_omp.cpp)

## Example CUDA program
#cuda_add_executable(bandwidthTest bandwidthTest.cu)
