# Writing an image

The ultimate goal of this project is to write a series of pixels (colors) to a file, for example a PNG file.

We can model a **file** as a 2D grid of pixels or colors. In reality, this grid is just a long array of pixels `width * height`.

Here is one way to model our image file (in `src/rayimage/Image.hpp`):

```cpp
#pragma once

#include <iostream>
#include "../raymath/Color.hpp"

class Image
{
private:
  unsigned int width = 0;
  unsigned int height = 0;
  std::vector<Color> buffer;
public:
  Image(unsigned int w, unsigned int h);
  Image(unsigned int w, unsigned int h, Color c);
  ~ Image();

  void SetPixel(unsigned int x, unsigned int y, Color color);
  Color GetPixel(unsigned int x, unsigned int y);

  void WriteFile(const char* filename);
};
```

And here is the implementation (`src/rayimage/Image.cpp`):

```cpp
#include <iostream>
#include "Image.hpp"
#include "../lodepng/lodepng.h"


Image:: Image(unsigned int w, unsigned int h) : width(w), height(h)
{  
  buffer.resize(width * height);
  for (int i = 0; i < buffer.size(); ++i) {
    buffer[i] = Color();
  }
}

Image:: Image(unsigned int w, unsigned int h, Color c) : width(w), height(h)
{  
  buffer.resize(width * height);
  for (int i = 0; i < buffer.size(); ++i) {
    buffer[i] = c;
  }
}

Image::~ Image()
{
}

void Image::SetPixel(unsigned int x, unsigned int y, Color color) {
  unsigned int index = (y * width) + x;

  if (index >= buffer.size()) { throw std::invalid_argument("Image: Invalid index"); }
  buffer[index] = color;
}

Color Image::GetPixel(unsigned int x, unsigned int y) {
  unsigned int index = (y * width) + x;

  if (index >= buffer.size()) { throw std::invalid_argument("Image: Invalid index"); }
  return buffer[index];
}


void Image::WriteFile(const char * filename) {
  std::vector<unsigned char> image;
  image.resize(width * height * 4);
  for(unsigned index = 0; index < buffer.size(); index++) {
    Color pixel = buffer[index];
    int offset = index * 4;

    image[offset] = (unsigned int)floor(pixel.R() * 255); 
    image[offset + 1] = (unsigned int)floor(pixel.G() * 255); 
    image[offset + 2] = (unsigned int)floor(pixel.B() * 255); 
    image[offset + 3] = 255;      // Alpha
  }

  //Encode the image
  unsigned error = lodepng::encode(filename, image, width, height);

  //if there's an error, display it
  if(error) std::cout << "encoder error " << error << ": "<< lodepng_error_text(error) << std::endl;
}
```

How does this code work?

1. We use a constructor that reserves a list of `Color` objects. The number of elements in the list corresponds to the total number of pixels in the image.
2. We can define specific pixels using the `x` and `y` coordinates.
3. We can save this grid in an image. I use the [lodepng](https://lodev.org/lodepng/) tool, which I downloaded and placed in the `src/lodepng` directory.

Remember that an image file is just a list of pixels, and each pixel is just a list of 3 numbers (one byte each). So our write function will just loop over each `Color`, and for each component of the color, convert the float value to a byte value and insert it into the final image array. A PNG file has a fourth component, alpha, which we are not using in this example, so we simply set it to its maximum value.

{% hint style="success" %}
I'll leave it to you to configure the CMakeLists.txt files! It's the same process we used for the Color class.
{% endhint %}

```cpp
#include <iostream>
#include "Color.hpp"
#include "Image.hpp"

using namespace std;


int main()
{    
    Color red(1, 0, 0);
    Color green(0, 1, 0);
    Color black;

    cout << "Red : " << red << std::endl;
    cout << "Green : " << green << std::endl;
    cout << "Black : " << black << std::endl;

    Color yellow = red + green;

    cout << "Yellow : " << yellow << std::endl;

    // Create an image in memory, and fill it with yellow
    Image image(512, 512, yellow);

    // Make a red square on the top left of the image
    for (int y = 0; y < 100; y++) {
      for (int x = 0; x < 100; x++) {
        image.SetPixel(x, y, Color(1, 0, 0));
      }
    }

    image.WriteFile("test.png");
}
```
