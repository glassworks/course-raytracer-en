# Linear Algebra

We need a way to represent rays and positions in our 3D world.

## Positions

We know that a two-dimensional position can be represented by the horizontal position `x` and the vertical position `y` in a simple vector form:

```
(x, y)
```

Thus, a point located 2 units to the right and 1 unit up would be:

```
(2, 1)
```

We can simply add a dimension or a third value to our vector to represent depth:

```
(x, y, z)
```

If the point above is actually 3 meters away (3 units on the z-axis):

```
(2, 1, 3)
```


## Directions

A direction can also be represented using a 3D vector. Let's imagine that we are at the origin and looking directly towards the positive x-axis. This direction can be represented as follows:

```
(1, 0, 0)
```

Or if the person is looking at the positive z-axis:

```
(0, 0, 1)
```

You may be a little confused. What is the difference between a position and a direction?

It all depends on how we interpret our vector.

Consider the vector `(1, 2)`. We could interpret it as a point in 3D space (a position):

![](./img/position.png)

We will also say that this same vector represents a direction that starts at `(0, 0)`:

![](./img/direction.png)

They have exactly the same shape, but very different meanings!

{% hint style="success" %}
In fact, a **position** in our virtual world can also be considered as the movement required to reach the destination if we started from the origin `(0,0,0)`.
{% endhint %}

A directional vector can be considered as the displacement required to move from position A to position B. It has two characteristics:

- a direction
- a magnitude (length)

Imagine that we are at point `(1, 1)` and we need to get to point `(4,5)`. We could move 3 units to the right and 4 units up. Our final movement can therefore be expressed by a vector `(3, 4)`. But we don't need to move to the right and up; we can simply walk straight ahead to our destination. It turns out that the magnitude of our trajectory is 5 units!

So we started at point `(1, 1)`, followed the movement `(3,4)`, and arrived at our destination `(4,5)`:

```
(1, 1) + (3, 4) = (4, 5)
```

Can you understand why I said we moved 5 units?

## Addition

Adding vectors is really interesting because a simple `+` between a point and a direction gives us a new point:

```
Point (1, 2) + Direction (1, -1) = New Point (2, 1)
```

![](./img/addition.png)

Or more simply:

```
(1, 2) + (1, -1) = (2, 1)
```

Thus, the geometric interpretation of adding a position vector to a direction vector consists of moving from the point to a final destination, following the movement expressed by the direction vector.

What about adding direction vectors? This is equivalent to adding a landmark to our journey. The resulting vector expresses the final movement from the first position to the destination, and its length is the shortest path between these two points.

## Subtraction

I am at point A and need to get to point B. What is the necessary movement?

This can be easily calculated by performing a subtraction!

Take the destination point (B) and subtract the starting point (A). The result is a directional vector that allows you to go from point A to point B.

```
Start: (1, 1)
End: (4, 5)

Displacement = End - Start
             = (4, 5) - (1, 1)
             = (3, 4)
```


## A Ray

What is a ray?

As with a ray of light, there is a source (its origin) and the direction in which the light will travel. The light will travel in this direction indefinitely!

We therefore express our ray using two values:


- `o`: an origin (a position)
- `d`: a **normalized** direction, i.e., with a length of one, which represents the direction of the line without specifying its length (because it is infinite!)

We can obtain any point on this ray by specifying the distance to be traveled, starting from the point of origin. Remember that the length of our direction vector is 1, so if we multiply it by any value, it will stretch to that value (example `1 * 5 = 5`).

```
// We want to travel t units in the direction of our ray
ray = o + (t * d)

// Example
o = (1, 1)
d = (0, 1)
t = 5

point on ray = (1, 1) + (5 * (0, 1))  
             = (1, 1) + (0, 5)
             = (1, 6)
```


## Normalization of a directional vector

Our vector math will be easier if the directional part of our ray has a length of 1. How do we force the directional vector to 1? Well, we divide by its length!

For example, if a vector has a length of 5, we know that `5 / 5 = 1`. So we just need to divide each component of our direction vector by 5.

But how do we get the length of a vector? Pythagoras!



![](./img/pythagorus.png)

Any direction vector can be expressed as a right triangle relative to the world axes. The length of this triangle is therefore:

$$
h^2 = x^2 + y^2
$$

Or:
$$
h = \sqrt{x^2 + y^2}
$$

We can therefore normalize the vector by dividing it by `h`:

```
d = (1, 2, 3)
length = sqrt(1*1 + 2*2 + 3*3)
dNormalized = (1 / length, 2 / length, 3 / length)

```


## Ray tracing

Let's return to our ray tracer. To simplify our calculations, let's place the camera at the origin `(0, 0, 0)`.

Let's say we want to project the scene onto a square plane located 1 unit away from the camera's z-axis:


![](./img/rays.png)

So we will pass a ray through each pixel:

```
ray00 = { o: (0, 0, 0), d: normalize(-1, 1, 1) }
ray01 = { o: (0, 0, 0), d: normalize(-0.666, 1, 1) }
ray02 = { o: (0, 0, 0), d: normalize(-0.333, 1, 1) }
...
ray10 = { o: (0, 0, 0), d: normalize(-1, 0.666, 1) }
ray11 = { o: (0, 0, 0), d: normalize(-1, 0.333, 1) }
...
```



{% hint style="success" %}

What happens if the camera is not at the origin? What happens if the camera is not oriented towards the positive z-axis?

Can you find the mathematical solution so that the series of rays is always projected?

{% endhint %}