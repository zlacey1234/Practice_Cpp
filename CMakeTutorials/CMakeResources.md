# CMake Resources

## Introduction

The CMake tutorial provides a step-by-step guide that covers common build system issues that CMake helps address. Seeing how various topics all work together in an example project can be very helpful.

**References:**
1. [CMake Tutorials](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)

## Step #1

### Building a Basic Project

The most basic CMake project is an executable built from a single source code file. For simple projects like this, a `CMakeLists.txt` file with three commands is all that is required.

Any project's top most CMakeLists.txt must start by specifying a minimum CMake version using the **`cmake_minimum_required()`** command. This establishes policy settings and ensures that the following CMake functions are run with a compatible version of CMake.

To start a project, we use the **`project()`** command to set the project name. This call is required with every project and should be called soon after **`cmake_minimum_required()`**. As we will see later, this command can also be used to specify other project level information such as the language or version number.

Finally, the **`add_executable()`** command tells CMake to create an executable using the specified source code files.

``` CMake
cmake_minimum_required(VERSION 3.10)

project(Tutorials)

add_executable(Tutorials tutorial.cxx)
```

### Specifying the C++ Standard

CMake has some special variables that are either created behind the scenes or have meaning to CMake when set by project code. Many of these variables start with `CMAKE_`. Avoid this naming convention when creating variables for your projects. Two of these special user settable variables are **`CMAKE_CXX_STANDARD`** and **`CMAKE_CXX_STANDARD_REQUIRED`**. These may be used together to specify the C++ standard needed to build the project.

This can be done using the **`set()`** function.

Example: C++20 Standard

``` CMake
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)
```

### Adding a Version Number and Configured Header File

Sometimes it may be useful to have a variable that is defined in your `CMakelists.txt` file also be available in your source code. In this case, we would like to print the project version.

One way to accomplish this is by using a configured header file. We create an input file with one or more variables to replace. These variables have special syntax which looks like `@VAR@`. Then, we use the **`configure_file()`** command to copy the input file to a given output file and replace these variables with the current value of VAR in the CMakelists.txt file.

While we could edit the version directly in the source code, using this feature is preferred since it creates a single source of truth and avoids duplication.

