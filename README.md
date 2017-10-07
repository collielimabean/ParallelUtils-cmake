ParallelUtils.cmake
========================

Template and some utilities for setting up a new CMake project with CUDA, MPI, and/or OpenMP

## Usage
Copy all files into your homework directory. 

First, open CMakeLists.txt and uncomment any libraries you need 
(e.g. OpenMP). Next, feel free to add any packages at the top of 
the file (e.g. threads, etc) as well as compiler-specific options.
If you use a compiler not on the list, please add it. 

If you have specific directories you need to include, do it on line 48.

After that, call `add_executable(exec_name exec_src1 exec_src_2)` to
allow CMake to build your binaries. Then, head to the command line:

```
[wjen@euler HW05]$ mkdir build
[wjen@euler HW05]$ cd build/
[wjen@euler build]$ cmake ..
-- The C compiler identification is GNU 7.1.0
-- The CXX compiler identification is GNU 7.1.0
-- Check for working C compiler: /usr/local/gcc/7.1.0/bin/gcc
-- Check for working C compiler: /usr/local/gcc/7.1.0/bin/gcc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/local/gcc/7.1.0/bin/g++
-- Check for working CXX compiler: /usr/local/gcc/7.1.0/bin/g++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found OpenMP_C: -fopenmp (found version "4.5")
-- Found OpenMP_CXX: -fopenmp (found version "4.5")
-- Configuring done
-- Generating done
-- Build files have been written to: /srv/home/wjen/759--collielimabean/HW05/build
[wjen@euler build]$ cmake --build .
Scanning dependencies of target problem2
[ 25%] Building CXX object CMakeFiles/problem2.dir/problem2.cpp.o
[ 50%] Linking CXX executable ../problem2
[ 50%] Built target problem2
Scanning dependencies of target problem1
[ 75%] Building CXX object CMakeFiles/problem1.dir/problem1.cpp.o
[100%] Linking CXX executable ../problem1
[100%] Built target problem1
[wjen@euler HW05]$ ls
build  CMakeLists.txt  Makefile  math.hpp  ParallelUtils.cmake  picture.inp  problem1  problem1.cpp  problem1_example.out problem2  problem2.cpp  stopwatch.hpp
[wjen@euler HW05]$
```
Note that problem1 and problem2 are in the HW directory.

Your binaries will be located in the expected place - top level of the homework folder. 

## Remarks
* I explictly disabled invoking cmake from the same directory as your source files.
This prevents you from clogging your source directory with full of CMake build
artifacts. It also makes it super easy to clean and exclude from git repositories.
* Some may wonder I did not invoke `make`. It's not cross-platform. The command
`cmake --build .` will invoke MSBuild on Windows, for example.
* Speaking of Windows, you should not invoke `cmake ..` like I do in the example.
CMake will default to a 32 bit build. To get around it, pass in 
`cmake -DCMAKE_GENERATOR_PLATFORM=x64 ..`. Clunky, I know.
* I added a `enable_intel_avx` macro in the ParallelUtils.cmake. 
* For Visual Studio users, you can technically stop at the `cmake ..` step. If 
you go into the build/ folder, you will see a .sln file, which you can open in
Visual Studio and build via the GUI.

