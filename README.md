ceres
=====

The project simply aggregates the projects needed to build a working version of Ceres on a Windows platform (together with build instructions!)

This repository contains git submodules. In order to clone it appropriately the submodules need to be initialized

```shell
git clone git@github.com:olivergardiner/ceres.git
cd ceres
git submodule update --init --recursive
```

An alternative to building Ceres from source is to use Microsoft's vcpkg (https://github.com/microsoft/vcpkg) to compile and install Ceres - a possible advantage of this approach is that it will build Ceres with a variety of configurations (e.g. with SuiteSparse) that are otherwise hard to build on Windows using CMake. However, the components included here will build a version of Ceres (using just Eigen) that is perfectly suited to the type of model fitting needed for modelling thermionic valves.

How to build with CMake
============

Open a PowerShell window in the ceres-window folder

```shell
mkdir build
cd build

mkdir gflags
cd gflags
cmake -DCMAKE_INSTALL_PREFIX=<Install path>/gflags -DCMAKE_BUILD_TYPE=Release ../../gflags
cmake --build . --target install --config Release

cd ..
mkdir glog
cd glog
cmake -DCMAKE_INSTALL_PREFIX=<Install path>/glog -DCMAKE_BUILD_TYPE=Release ../../glog
cmake --build . --target install --config Release

cd ..
mkdir Eigen
cd Eigen
cmake -DCMAKE_INSTALL_PREFIX=<Install path>/eigen3 -DCMAKE_BUILD_TYPE=Release ../../Eigen
cmake --build . --target install --config Release

cd ..
mkdir lapack
cd lapack
cmake -DCMAKE_INSTALL_PREFIX=<Install path>/lapack -DCMAKE_BUILD_TYPE=Release ../../lapack
cmake --build . --target install --config Release

cd ..
mkdir ceres-solver
cd ceres-solver
cmake -DCMAKE_INSTALL_PREFIX=<Install path>/ceres-solver -DCMAKE_BUILD_TYPE=Release ../../ceres-solver
cmake --build . --target install --config Release

```
