---
layout: docs
title: Vector
prev_section: point
next_section: home
permalink: /docs/vector/
---

Vectors are very similar to points, the difference is that a vector represents 
a direction and magnitude. Examples of vectors mightbe gravity, the force of a
friction, or the velocity and direction of a bullet.


## Usage
--------
{% highlight javascript %}
var vector = new Vector(2, 4);

// Distance from the origin == magnitude of a vector
var magnitude = vector.distance();

// A "normal" is a vector with a magnitude of 1.
var normal = vector.normalize();

// Scaling a vector increases it's magnitude
var vectorLength3 = vector.normalize().scale(3);

var addedVector = vector.add(new Vector(2, 0));
console.log("x, y:", addedVector.x, addedVector.y);
// x, y: 4 4

var subVector = vector.minus(new Vector(2, 3));
console.log("x, y:", subVector.x, subVector.y);
// x, y: 0, 1

var dotproduct = vector.dot(new Vector(1, 1));
console.log("Dot product", dotproduct);
// Dot product 8

// Perpendicular vectors have a crossproduct of 0
var crossproduct = vector.cross(4, 2);
console.log("Cross Product", crossproduct);
// Cross Product 0

{% endhighlight %}


## Constructor 
<pre>new(x : number, y : number)</pre>
--------------

The Vector constructor takes an x representing the magnitude and direction in x, and
it takes a y representing the magnitude and direction in y.

## Properties
<pre>vector.x</pre>
--------------

The x component of the vector.

<pre>vector.y</pre>
--------------

The y component of the vector.

## Methods
<pre>vector.distance(v? : Vector) : number</pre>
--------------

Calculate the distance from this vector to another. If no other vector is specified
the distance from the origin will be returned.

<pre>vector.normalize() : Vector</pre>
--------------

Return a new vector pointing in the same direction as the original, with a 
magnitude of 1.

<pre>vector.scale(size : number) : Vector</pre>
--------------

Return a new vector who's magnitude is "size" times bigger.

<pre>vector.add(v : Vector) : Vector</pre>
--------------

Return a new vector who's x and y components are the
sum of both vectors.

<pre>vector.minus(v : Vector) : Vector</pre>
--------------

Return a new vector who's x and y components are the
difference of the original vector and the "v" vector.

<pre>vector.dot(v : Vector) : number</pre>
--------------

Return the dot product between these two vectors.


<pre>vector.cross(v : Vector) : number</pre>
--------------

Return the 2D scalar cross product between these vectors. Vectors that are 
perpendicular (at a right angle) have a cross product of 0.







