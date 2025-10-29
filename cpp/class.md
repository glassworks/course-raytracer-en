# Class

A class is the central principle of the object-oriented programming paradigm and will be very useful for the architecture of our raytracer.

We will use classes for our mathematical modeling, which will greatly facilitate our operations.

For this example, we will model a **color**, which is simply a vector (or **tuple**) containing three values: red, green, and blue:
 

```
(r, g, b)

Red = (1, 0, 0)
Green = (0, 1, 0)
Blue = (0, 0, 1)
Yellow = (1, 1, 0)
....
White = (1, 1, 1)
Black = (0, 0, 0)
```

Have you ever heard of a **pixel**? It's actually a tuple containing the three floating point values for red, green, and blue!

In C++, we manage dependencies by first specifying the *interfaces* of our classes (using **h** files), and then implementing those interfaces in **cpp** files.

Let's define our interface to represent a color (in `src/raymath/Color.hpp`):


```cpp
#pragma once

#include <iostream>

class  Color
{
private:
  float r = 0;
  float b = 0;
  float g = 0;
public:
  Color();
  Color(float r, float g, float b);
  ~ Color();

  float R();
  float G();
  float B();

  Color operator+(Color const& col);
  Color& operator=(Color const& col);
  friend std::ostream & operator<<(std::ostream & _stream, Color const & col);
};
```

We define three private values, `r`, `g`, and `b`. We also define two constructor functions:

- One that initializes the color to black
- Another that takes three parameters and initializes the color accordingly.
  
It is always a good idea to include a **destructor** function—the function that will be called when the object instance is destroyed (to clean up the memory).

We have defined two **operators** that will make our lives easier when using this class:

- `+`: which will allow us to use the `+` symbol between two objects of type `Color`, thus performing the color equivalent of an addition.
- `<<`: which will allow us to serialize our `Color` in an `iostream` to facilitate debugging.

Now let's look at the implementation (in `src/raymath/Color.cpp`):


```cpp
#include <iostream>
#include <cmath>
#include "Color.hpp"

Color:: Color() : r(0), b(0), g(0)
{  
}

Color:: Color(float iR, float iG, float iB) : r(iR), g(iG), b(iB)
{  
}

Color::~ Color()
{
}

float Color::R()
{
  return r;
}

float Color::G()
{
  return g;
}

float Color::B()
{
  return b;
}

/**
 * Implementation of the + operator :
 * Adding two colors is done by just adding the different components together :
 * (r1, g1, b1) + (r2, g2, b2) = (r1 + r2, g1 + g2, b1 + b2)
 */
Color Color::operator+(Color const& col) {
  Color c;
  c.r = fmax(fmin(r + col.r, 1), 0);
  c.g = fmax(fmin(g + col.g, 1), 0);
  c.b = fmax(fmin(b + col.b, 1), 0);
  return c;
}

/**
 * Overriding the assignment operator
 */
Color& Color::operator=(Color const& col) {
  r = col.r;
  g = col.g;
  b = col.b;
  return *this;
}

/**
 * Here we implement the << operator :
 * We take each component and append it to he stream, giving it a nice form on the console
 */
std::ostream & operator<<(std::ostream & _stream, Color const & col) {  
  return _stream << "(" << col.r << "," << col.g << "," << col.b << ")";
}
```

## Compiling this library

We want to develop a number of classes such as `Color` in our project. It is useful to group them together in a **library**.

In CMake, we proceed as follows:

1. Add the file `src/raymath/CMakeLists.txt`, with the instruction to build our new class:


```cmake
add_library(raymath 
  ${CMAKE_CURRENT_SOURCE_DIR}/Color.cpp
)
```

2. Modify our root file `CMakeLists.txt`.


```cmake
cmake_minimum_required(VERSION 3.5.0)
project(raytracer VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_executable(raytracer main.cpp)

# Add these lines
target_include_directories(raytracer PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           "${PROJECT_SOURCE_DIR}/src/raymath"
                           )

add_subdirectory(./src/raymath)

target_link_libraries(raytracer PUBLIC raymath)
```

## Using the library

We can now use our `Color` class in our project:

```cpp
#include <iostream>

// Include our class definition - we can read it thanks to `target_include_directories`
#include "Color.hpp"

using namespace std;

int main()
{    
    Color red(1, 0, 0);
    Color green(0, 1, 0);
    Color black;

    // We can chain our color instances using << thanks to our operator !
    cout << "Red : " << red << std::endl;
    cout << "Green : " << green << std::endl;
    cout << "Black : " << black << std::endl;

    // We can perform an addition + operation thanks to our operator !
    Color yellow = red + green;

    cout << "Yellow : " << yellow << std::endl;    
}

```
