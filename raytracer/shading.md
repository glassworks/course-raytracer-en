# Shading



Remember that we are trying to calculate the color of a pixel.

Let's assume that our pixel starts out black:


```
let pixel = (0, 0, 0)
```

If we cast a ray and it doesn't hit anything in the scene, the pixel remains black and we move on to the next pixel.

However, if we hit an object, we can give the pixel the **ambient color** of that object.

Suppose we encounter a sphere and we know that this sphere is a dark green color:


```

let pixel = (0, 0, 0)
let ray = { o: Vector3, d: Vector3(normalized) }
let sphere = { c: Vector3, r: float, ambientColor: Color }

let P = intersectSphere(ray, sphere)

if (!P) { return }   // no intersection 

// Add the base color of the sphere
pixel = pixel + sphere.ambientColor

```

Implement this algorithm in your code, and you will have implemented a **flat shader**!

{% hint style="success" %}
A **flat shader** does not give any 3D effect to the surface. In reality, it is the light reflected by an object that gives it its depth in the real world.
{% endhint %}


## Diffuse Shader

It is the light in our scene that gives our objects their depth. We must take into account the light and shape on the surface of our intersection point.

![](./img/diffuse.png)

In the image above, we have already calculated that our ray intersects the sphere at point P. Now we want to know the color of the sphere at point P.

A simple shading model is to say that the color of the point is relative to the angle between the incoming light and the normal at the point.

The smaller the angle, the more directly the light hits the surface. The larger the angle, the less directly the light hits the surface.

Looking at the diagram, we can calculate the normal of a sphere, which is simply the vector `cp`.


```
let cp = p - sphere.c
```

The vector pointing to the light is just the position of the light subtracting the point:

```
let pl = l - p
```

Once again, the dot product comes to our rescue! Remember we said that if the dot product of two vectors is 0, then they are perpendicular? It follows that if the dot product is 1, then the two vectors are parallel.

So we can use the dot product as an intensity multiplier! If the angle with the light is perpendicular, the value of the dot product is 0, so we multiply the color of our object by zero (black). If the angle with the light is 0 degrees, the value of the dot product is 1, so we multiply the color of our object by 1.
 

```
let nCP = normalize(cp);
let nPL = normalize(pl);

let intensity = dotProduct(nCP, nPL);

pixel = pixel + intensity * sphere.ambientColor

```

## Shading models

There are, of course, many different shading models. We have just started with the model called “Phong.” Try implementing your own!


- [Phong](https://en.wikipedia.org/wiki/Phong_reflection_model)
- [Blinn-Phong](https://en.wikipedia.org/wiki/Blinn–Phong_reflection_model)
- [Cook Torrance](https://garykeen27.wixsite.com/portfolio/cook-torrance-shading)


## Shadows

How do we take shadows into account?

What is a shadow? It is the absence of light, due to the fact that there is an obstacle between the light and a surface.

This fits perfectly with our concept of raytracing! 

Before calculating the impact of light on our pixel (using the `pl` vector in our example above), perhaps we should first check whether there is another object between the pixel and the light.

How can we do this? Fire a ray! If our ray crosses another object in the scene before reaching the light, this means that our pixel should not receive any value from this light: it is in the shadow!