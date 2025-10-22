# Intersections

We now have a mathematical construct to represent a Ray.


```
// Our ray
ray = {
  o: (0, 0, 0)
  d: (dx, dy, dz)
}
```

The purpose of our ray tracer is to calculate whether this ray intersects with objects in our 3D virtual world!

How do we perform this calculation?

## Intersection with a sphere

The surface of a sphere can be defined parametrically as a point in space (let's call it `c` for **center**) and a radius (`r`). The surface is the infinite number of points located at `r` units from the center `c`.

Consider the following configuration. We want to know if the red ray will eventually intersect the sphere:

![](img/sphere-intersection.png)

How can we do this?

Well, there are certain things we know:

* We know the origin of our ray: `o`
* We know the center of the circle: `c`.

Knowing these two positions, we can calculate a vector that represents the distance to travel from `o` to `c`, using subtraction:

```
oc = c - o
```

![](img/sphere-intersection-2.png)

If we **project** `OC` onto our ray, we get point `P`, which will fall somewhere along the ray (the dotted part of the line represents the part of the ray that is beyond the first unit represented by our normalized direction).

Fortunately, it is easy to project one vector onto another normalized vector using the **dot product**. Imagine we have one vector `d` and another `n`. To project vector `d` onto normalized vector `n`, we use the formula:


$$
proj(d,n) = (\bar{d}\cdot\bar{n})\bar{n}
$$

The dot product is easy to calculate :

```
let d = (dx, dy, dz)
let n = (nx, ny, nz)

let dotproduct = (dx * nx) + (dy * ny) + (dz * nz)
```

Thus, in our example, the projection can be calculated as follows:

```
ray = {
  o: (0, 0, 0)
  d: (x, y, z)
}
sphere = {
  c: (cx, cy, cz)
  r: 5
}

oc = sphere.c - ray.o

// Calculate the dot product which is just a float
dotProd = (oc.x * ray.d.x) + (oc.y * ray.d.y) + (oc.z * ray.d.z);

// Multiply the dot product with the ray's direction vector
op = dotProd * ray.d = (dotProd * ray.d.x, dotProd * ray.d.y, dotProd * ray.d.z)

```

Thus, `op` is the vector that takes us from `o` to `p`.

To calculate the actual value of P, we start from the origin of our radius and add our vector!

```
p = o + op
```

That's great, but how does knowing the position of `p` help us? If it is inside the sphere, we know that it undoubtedly intersects it. How can we tell if it is inside the sphere? It's simple! If the distance between `c` and `p` is less than or equal to the radius of the sphere!

How do you calculate the distance between two points? Well, you calculate the movement required to go from one to the other (subtraction), and you calculate the length of this vector (Pythagoras).

```
// Displacement vector from c to p
cp = p - c

// calculate the length of a vector using pythagorus !
let distance = length(cp) 

if (distance < r) { 
  // Intersects sphere!
} else {
  // No intersection
}
```

Great! We know there is an intersection! How do we find the exact intersection point `p1`?

![](img/sphere-point-of-intersection.png)

We already know the length of `cp`, we know the value of `r`, and so using Pythagoras we can calculate the length of `p -> p1` (let's call it `a`).

```
let distance = length(cp) 
let a = sqrt( r*r - distance*distance )
```

To obtain position `P1`, simply move back `a` units along our initial radius, but in the opposite direction:
```
let p1 = p + (a * (-d))
```

There you go!

Now that we know the exact position of P in the world, we can start determining the color of the surface at that point!

Here is a pseudo-code summary of the calculations needed to calculate the intersection point:

```
struct Vector3 {
  x: float
  y: float
  z: float
}

// calculate the length of a vector
function length(a: Vector3) {
  float l = Math.sqrt(a.x*a.x + a.y*a.y + a.z*a.z);
  return l
}

// normalise a vector (divide by its length)
function normalize(a: Vector3) {
  float l = length(a);
  return (a.x / l, a.y / l, a.z / l)
}

// calculate the dot product between two vectors
function dotProduct(a: Vector3, b: Vector3) {
  return (a.x * b*x) + (a*y + b*y) + (a.z * b.z)
}

let ray = { o: Vector3, d: Vector3(normalized) }
let sphere = { c: Vector3, r: float }

function intersectSphere(ray, sphere) {
  
  let OC = sphere.c - o      // OC is a vector

  let dotProd = dotProduct(OC, ray.d)   // dotProd is a float

  let OP = dotProd * ray.d      // OP is a vector

  let P = ray.o + OP            // P is a point

  let CP = P - sphere.c                // CP is a vector

  let lenCP = length(CP)        // lenCP is a float

  // No intersection if the distance from between P and C 
  // is greater than the radius of our sphere!
  if (lenCP > sphere.r) { return }   

  let a = Math.sqrt(r*r - lenCP*lenCP)    // a is a float

  let P1 = P + (a * -ray.d)               // P1 is a vector

  return P1
}
```

{% hint style="success" %}

Here are some figures to help you debug your implementation.

Let's imagine we have a camera at `(0,0,0)`, oriented towards the negative z-axis.

For a sphere at `(0, 0, 6)` with a radius of `1`:

- A ray passing through the point `(0, 0, 1)` will touch the sphere at `(0, 0, 5)`
- A ray passing through the point `(0.01, 0, 1)` will have the normalized direction `(0.0099995,0,0.99995)` and will touch the sphere at `(0.0500125,0,5.00125)`

For a sphere at `(2, 0, 6)` with a radius of `1`:

- A radius passing through the point `(0.5, 0.05, 1)` will have the normalized direction `(0.446767,0.0446767,0.893534)` and will touch the sphere at `(2.63852,0.263852,5.27704)`.

{% endhint %}

## Note on the dot product

The dot product between two vectors is a very interesting and useful value.

### Spatial relationship

If **both vectors are normalized**, the scalar product is equal to the **cosine** of the angle between the two vectors.

$$
\bar{d}\cdot\bar{n}= \cos{\theta}
$$

Why is this useful? Well, without having to calculate the angle θ, we can deduce things about the relationship between the two vectors.

![](img/Cosine-Graph.png)

The graph shows that:

* if the scalar product = 1, then we are at 0°. Both directions are oriented in the same direction
* if the scalar product = 0, then we are at 90°. Both directions are perpendicular.
* if the scalar product > 0, the graph is somewhere between 0° and 90°, so it must be an acute angle
* if the scalar product < 1, the graph is somewhere between 90° and 270°, so it must be an obtuse angle.

In the previous example, we wanted to know if the sphere was **in front of the ray** (and not behind it). The angle between our ray and the direction towards the center of the sphere must therefore be an acute angle. We calculate the dot product between these two (normalized) directions, and if it is negative, we know that it is an obtuse angle, and therefore that the sphere must be behind us!


```
// Normalise OC
ocnorm = normalise(oc)
// ray.d - should be already be normalised !

// If the dotproduct is negative, the angle between the two directions is
// greater than 90°, so the object must be behind the ray. Ignore the object!
if (dotproduct(ocnorm, d) < 0 ) { return }
```

### Angle

We can, of course, obtain the angle (in radians) between the two directions using the inverse cosine:

$$
\theta = \arccos({\bar{d}\cdot\bar{n}})
$$

This method returns a value between 0 and 2π. However, it does not return negative numbers, so we cannot tell whether the angle between the two vectors is to the left or to the right.

{% hint style="info" %}

How do you convert radians to degrees?

$$
degrees = radians * 180/\pi
$$
{% endhint %}

### Projection

The dot product between an unnormalized vector and a normalized vector gives us the length of a projection of the unnormalized vector onto the normalized vector.

What is a projection?

Imagine that you are projecting light perpendicularly onto the normalized vector. The shadow of the other vector on the normalized vector is the projection!

Imagine we have a vector `d` and another vector `n` (which is normalized). To project vector `d` onto vector `n`, we use the formula:

$$
proj(d,n) = (\bar{d}\cdot\bar{n})\bar{n}
$$

## Intersection with a plane

An infinite plane can be expressed parametrically as follows

* suppose we have a point `c` in space, and a normal vector `n`
* the plane is the set of points `p` where the vector `pc` is perpendicular to the normal `n`.

![](img/plane-intersection.png)

In the diagram, we assume that `p` is also on our ray. If the direction of the ray is normalized, we just need to find a multiplier `t` for this ray that will resize it enough to bring us to `p`.

$$
\bar{p} = \bar{o} + t\bar{d}
$$

We don't know what `t` is yet—we have to calculate it!


But we need more information.

Looking at the diagram, we can also deduce that if `p` is on the plane, then the line `pc` must be perpendicular to the normal `n`.
Fortunately, the dot product is our friend again! Indeed, if the dot product between two normalized vectors is 0, it means that the two vectors that created it are perpendicular!

$$
(\bar{p} - \bar{c})\cdot(\bar{n}) = 0
$$

Let's replace `p` in our radius with the formula for the plane:

$$
(\bar{o} + t\bar{d} - \bar{c})\cdot\bar{n} = 0
$$

Multiply the dot product:

$$
\bar{o}\cdot\bar{n} + t\bar{d}\cdot\bar{n} - \bar{c}\cdot\bar{n} = 0
$$

Solve for `t`:

$$
t\bar{d}\cdot\bar{n} = \bar{c}\cdot\bar{n} -\bar{o}\cdot\bar{n}
$$

$$
t\bar{d}\cdot\bar{n} = (\bar{c} -\bar{o})\cdot\bar{n}
$$

$$
t = \frac{(\bar{c} -\bar{o})\cdot\bar{n}}{\bar{d}\cdot\bar{n}}
$$

So we have a relatively simple formula for calculating `t`!

Let's first calculate the denominator:

```
let denom = dotProduct(ray.d, plane.n)

if (denom > -0.000001) {
  // The ray is parallel to the plane (denom == 0)
  // OR The angle between the the incoming ray and the normal is > 90°
  //    meaning the plane is behind us
  return
}
```

If the denominator is zero or close to zero, this means that our radius is perpendicular to the normal, i.e., the radius is parallel to the plane and will never intersect it!

Next, let's calculate the numerator:

```
let num = dotProduct(plane.c - ray.o, plane.n)

let t = num / denom
```

Now that we have `t`, we can calculate point `p` by substituting it into our radius formula:

```
let p = ray.o + t * ray.d
```

All together :

```

let ray = { o: Vector3, d: Vector3(normalized) }
let plane = { c: Vector3, n: Vector3(normalized) }

function intersectPLane(ray, plane) {
  
  let denom = dotProduct(ray.d, plane.n)

  if (denom > -0.000001) {
    // The ray is parallel to the plane
    return
  }
  let num = dotProduct(plane.c - ray.o, plane.n)

  let t = num / denom

  let p = ray.o + t * ray.d

  return p

}
```
