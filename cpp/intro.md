# A simple project

This is a short guide to help you get started with your first C++ project. A sample project is available at [https://dev.glassworks.tech/courses/raytracer/raytracer-sample](https://dev.glassworks.tech/courses/raytracer/raytracer-sample).

You are free to use the software environment of your choice, but this guide will help you use Visual Studio Code.

## Extension VS Code

Visual Studio Code has excellent support for C++. You can [follow this guide](https://code.visualstudio.com/docs/languages/cpp) to install the extension.

You will need to install a C++ compiler (if it is not already present) for your operating system:

* [gcc on Windows](https://code.visualstudio.com/docs/cpp/config-mingw)
* [cmake on macOS](https://code.visualstudio.com/docs/cpp/config-clang-mac)

In general, there are excellent tutorials for getting started with C++ [on this website](https://code.visualstudio.com/docs/cpp/introvideos-cpp)

## A “hello world” program

This small example comes from the VSCode guides.

* [CMake for Linux](https://code.visualstudio.com/docs/cpp/cmake-linux#\_build-hello-world)
* [Cmake](https://code.visualstudio.com/docs/cpp/cmake-quickstart)

We just want to create a simple executable that prints a message to the console. Create the file `main.cpp`:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{
    vector<string> msg {"Hello", "C++", "World", "from", "VS Code", "and the C++ extension!"};    

    for (const string& word : msg)
    {
        cout << word << " ";
    }
    cout << endl;
}
```

Your group may have developers who use multiple operating systems. We will try to create a cross-platform build system using CMake.

First, install [CMake tools for VSCode](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools).
Once installed, open the VSCode Command Palette (`cmd+shift+P` or `F1`), type `CMake`, and choose `CMake: Quick Start`. Answer the following questions:

* Enter a project name
* Choose C++
* Do not select CTest or CPack
* Select “Executable” (not library)

This will create the `CMakeLists.txt` file, which tells CMake how to build your project.

To use a modern version of C++, we need to enable at least version 11:

```txt
cmake_minimum_required(VERSION 3.5.0)
project(raytracer VERSION 0.1.0 LANGUAGES C CXX)

# !!! ajoutez ces 2 lignes !!!
set (CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)


# change main.cpp to the entry file of your project -the one that has "int main() {}"
add_executable(raytracer main.cpp)
```

Launch the command palette again (`F1`), type `CMake: Quick Start`, which will continue the process, asking you how you want to compile your project (create a `preset`).

Select `Add a preselection`, then `Create from compilers`. A list of compilers available on your machine will be displayed. Choose one.

Then give your preselection a name, such as `macos-clang`, or something you can reuse.

You will see the `CMakePresets.json` file appear, containing your configuration.

Each team member may need to add their own preset depending on their architecture.

Once configured, you will see options in the bottom bar to build and run your application:

![](img/build.png)

Alternatively, you can navigate to the `build` or `out` directory and type:

```bash
make
```

This will generate your executable in the same directory. I named mine `raytracer`, so I can launch it using:

```bash
./raytracer
```

If you run your project, you should see the output in the terminal:

```
Hello C++ World from VS Code and the C++ extension! 
```
