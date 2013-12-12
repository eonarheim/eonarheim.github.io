---
layout: docs
title: Color
prev_section: logger
next_section: spritesheet
permalink: /docs/color/
---

Excalibur provides a simple abstraction over colors for the canvas that allows
RGB, RGBA, or HEX input.

## Usage
--------

{% highlight javascript %}

var color = new Color(255, 255, 0, .5);
// or
var color1 = Color.fromRGB(255, 255, 0, .5);
// or
var color2 = Color.fromHex("#ffff007f");

// Call toString() when setting styles
game.ctx.fillStyle = color.toString();

{% endhighlight %}

## Constructor
<pre>new(public r : number, 
    public g : number, 
    public b : number, 
    public a? : number)</pre>
----------

The Color constructor takes 3 required paramenters, each a number between 0-255
representing red, green, and blue. The 4th optional parameter specifies the 
alpha value betwen 0 and 1. An alpha of 1 means the color is completely opaque and
a value of 0 means the color is completely transparent.

## Static Constants

<pre>Color.White</pre>
<pre>Color.Black</pre>
<pre>Color.Yellow</pre>
<pre>Color.Orange</pre>
<pre>Color.Red</pre>
<pre>Color.Vermillion</pre>
<pre>Color.Rose</pre>
<pre>Color.Magenta</pre>
<pre>Color.Violet</pre>
<pre>Color.Blue</pre>
<pre>Color.Azure</pre>
<pre>Color.Cyan</pre>
<pre>Color.Viridian </pre>
<pre>Color.Green</pre>
<pre>Color.Chartreuse</pre>
<pre>Color.Transparent</pre>
----------

Excalibur comes with a number of predefined static color constants accessible off of the Color type.


## Static Methods
<pre>Color.fromRBG(r : number, g : number, b : number, a? : number) : Color</pre>
------------

<pre>Color.fromHex(hex : string) : Color</pre>
------------

## Properties
<pre>color.r</pre>
------------

Get or set the red component of the current color instance between 0-255.

<pre>color.g</pre>
------------

Get or set the green component of the current color instance between 0-255.

<pre>color.b</pre>
------------

Get or set the blue component of the current color instance between 0-255.

<pre>color.a</pre>
------------

Get or set the alpha value of the current color instance between 0-1. An alpha
of 1 means the color is completely opaque, and an alpha of 0 means the color is
completely transparent.

## Methods
<pre>color.toString()</pre>
-----------

Returns a color string that the DOM or native draw code can understand. This is important
to use when directly operating on the canvas context or setting styles in the DOM.





