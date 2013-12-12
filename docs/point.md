---
layout: docs
title: Point
prev_section: topcamera
next_section: vector
permalink: /docs/point/
---

A Point is a 2D representation of an x and y coordinate on the screen.

## Usage
--------
{% highlight javascript %}
var point = new Point(2, 4);

console.log(point.x);
// 2

console.log(point.y);
// 4

{% endhighlight %}


## Constructor 
<pre>new(x : number, y : number)</pre>
--------------

The Point constructor takes the x and y coordinate as its arguments.

## Properties
<pre>point.x</pre>
--------------

The x coordinate of the point in 2D space.

<pre>point.y</pre>
--------------

The y coordinate of the point in 2D space.