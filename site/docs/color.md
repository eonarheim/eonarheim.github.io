---
layout: docs
title: Color
prev_section: actor
next_section: none
permalink: /docs/color/
---

Excalibur provides a simple abstraction over colors for the canvas that allows
rgb, rgba, or hex input.

## Usage
--------

{% highlight javascript %}

var color = new Color(255, 255, 0, .5);
// or
var color1 = Color.fromRBG(255, 255, 0, .5);
// or
var color2 = Color.fromHex("#ffff007f");

{% endhighlight %}

## Constructor
--------
<pre>new(public r : number, 
    public g : number, 
    public b : number, 
    public a? : number)</pre>

