# Principles

In photorealistic rendering, a _raytracer_ aims to simulate how light bounces around a three-dimensional virtual scene.

The goal is to render an image that looks as close to the real world as possible, hence the term “photorealistic.”

We simulate light — a physical phenomenon that involves frequencies, wavelengths, material properties, and so on. You will discover that trying to simulate a natural phenomenon on a computer is a difficult and often computationally expensive exercise (which makes it an excellent learning experience in the context of this course!).

When we _model_ real-life physics, to reduce the problem to a manageable level, we create a simplified version to start with. That's what we're going to do for light rays!

## A simplified model of light

Let's simplify how we perceive things in the real world, as illustrated in the following image:&#x20;

<figure><img src="img/light.png" alt=""><figcaption></figcaption></figure>

In its simplest form, a light (or the sun) emits light rays, which can be represented by a **directional vector**, a straight line that has a source and a direction.

This light travels in a straight line until it reaches an object in our world. Some of the wavelengths of light (colors) will be absorbed by the surface of the object, depending on its composition. Some surfaces, such as wood, absorb all colors except brownish colors. A sheet of white paper absorbs virtually no colors and reflects them all.

The light ray is reflected around the **normal to the surface** at the point of intersection with the object. A surface normal is the direction **perpendicular** to the surface. This reflected light ray continues on its way into the world. Perhaps the light ray enters our eye and lands on our retina. This is how we perceive things in our world! Based on the light that has bounced around the world, colors being absorbed or reflected along the way, and luckily entering our eyes.

## An inverted model for greater simplicity

It would be far too costly to simulate every ray of light emitted by a light source in a virtual scene, hoping to record only those that land on our virtual retina! We need to simplify the problem.

What if we reversed the problem? Let's ignore all the light that never enters our eye, and simulate only the light that does enter. This drastically reduces the number of rays to be calculated.

But how do we know which rays, starting from the light source, end up reaching our eyes?

Well, rays are just a series of straight lines that bounce around their normals. What works in one direction works just as well in the other!

This time, let's start the ray in our eye and send it into the scene. When we hit an object, we can determine the color of that object (at the point of intersection), calculate the new reflected ray, and repeat the process.

The final color that our virtual eye sees will simply be the color accumulated (i.e., the addition of colors) along the path traveled by our ray!

![](img/simple-raytracing.png)

## What is color?

In physics, color is light with a certain wavelength. This is a bit complicated, and we can model this entity more simply.

Our modern computer screens give us the impression of seeing images, photos, and movies by emitting light at different wavelengths. If you look closely at a computer screen, you will notice that it is a dense network of LED emitters of the three basic wavelengths: red, blue, and green (RGB). These three wavelengths can produce a **gamut** of colors ranging from almost black (no light) to white (maximum intensity).

Each triplet of red, green, and blue LEDs represents a **pixel**. If we arrange a row of 1920 tightly packed pixels horizontally, and do this for 1080 rows, we will have an HD screen of 1920x1080 pixels, or 1920x1080x3 LEDs!

RGB has become the standard unit of color representation in light-emitting devices, and this is the unit we will use here. What is a color in our context? It is the intensity of red, green, and blue for a single pixel! It is easy to represent using a three-dimensional tuple:

`(red, green, blue)`

We are free to decide in which range to represent each intensity (or **color depth**). For example, if we use 1 byte (i.e., a minimum of zero and a maximum of 255) to represent each intensity, we could have the following:

```
Red:   (255, 0, 0)
Green: (0, 255, 0)
Blue:  (0, 0, 255)
```

We could also normalize this value and say that we will represent each component as a floating point between 0 and 1:

```
Red:   (1, 0, 0)
Green: (0, 1 0)
Blue:  (0, 0, 1)
```

The advantage of this representation is that colors can be easily combined by simple addition!

What do you get when you mix red and green (in light, not paint!)? Yellow!

```
(1, 0, 0) + (0, 1, 0) = (1, 1, 0)
```

This is a simple vector addition, which consists of adding each component of the first vector to the corresponding component of the second vector.

However, there is a problem. We can never have a value greater than the maximum. Therefore, if we add turquoise to our yellow, we will simply get white (and not a strange color like octarine):

```
(1, 1, 0) + (0, 1, 1) = (1, 1, 1)   // and not (1, 2, 1)
```

## What is an image?

Our goal is to render an **image**, a two-dimensional plane onto which light from the world is projected.

We know that our image is composed of **pixels** (for example, 1920x1808 pixels in total).

An image is therefore just a huge array of color tuples.

```
[
  (0, 0, 1),
  (0, 0, 1),
  (1, 0, 1),
  (1, 1, 1),
]
```

The example above is a 2x2 image containing 4 pixels.

The goal of our raytracer is therefore to calculate the correct color for each pixel, so that it accurately represents a projection of the scene!

Once we have this table of RGB values, we just need to save it to a file (a bitmap, without compression, or a .png for lossless compression).

## An algorithm to generate our image

The following pseudocode can be used to generate an image:

```ts

let width = 1920
let height = 1080
let pixels = Array(1920x1080)

// The position of the camera in the world
const cameraPosition = (0, 0, -1)
// The direction of the camera
const cameraDirection = (0, 0, 1)

for (let y = 0; y < height; ++y) {
  for (let x = 0; x < width; ++x) {
    
    // Initially the color of the pixel is black
    let color = (0, 0, 0);

    // Get the world ray starting at the camera position, and going through the current pixel
    let direction = getWorldRay(x, y);

    // Cast the ray into the world
    color = color + castRay(cameraPosition, direction)

    // Set the pixel in the image
    pixels[(y * width) + x] = color;
  }
}

```

How do you get the **world ray**?

It's actually quite easy. We simply want to shoot a ray from our eye through each pixel of a virtual image in front of our eye:

![](img/image-ray.png)

Easy, right? Well... you might need a little math to implement this algorithm.
