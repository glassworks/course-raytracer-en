# Reflections
Once we have calculated the color at a point, we may want to accumulate the reflections from other objects at that point.

To do this, we need to cast a ray in a direction around the normal.

```
pixel = pixel + castRay(P, reflectDirection)
```

We repeat the ray tracing process and add the reflected color to the current color. In reality, we would apply a multiplier to attenuate the reflection color:


```
pixel = pixel + sphere.reflectFactor * castRay(P, reflectDirection)
```

But how do you calculate the direction of reflection?

Consider the image:

![](./img/reflection1.png)

We need to calculate the vector `pr`, which is a reflection of `op` around the normal `n`.

How do we do this?

First, let's project `Ppr` onto the normal:
 

![](./img/reflection2.png)

Now let's invert this projection (by multiplying it by -1) and double it:


![](./img/reflection3.png)

If we add our original direction vector to our projection, we get `r`!

![](./img/reflection4.png)

In code, our reflection vector is calculated as follows:

```
let normal = normlize(P - sphere.c);

function reflectRay(ray, normal, P) {
  // project the ray direction onto the normal
  let proj = dotProduct(ray.d, normal) * normal

  // invert the projection and multiply by 2
  proj = -2 * proj

  let reflectDir = proj + ray.d  

  // The new ray has P as its starting point, and the reflectDir as its direction
  return new Ray(
    o = P
    d = reflectDir
  )
}

```