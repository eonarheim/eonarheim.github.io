---
layout: docs
title: Sprite
prev_section: spritesheet
next_section: animation
permalink: /docs/sprite/
---

A Sprite is just an image that represents a smaller piece of a bigger image, 
known as a sprite sheet. Sprites are useful for providing static images to
a game.

## Usage
--------
{% highlight javascript %}
// Load image into Excalibur
var game = new Engine();
var loader = new Loader();
var image = new PreloadedImage("image.png");
loader.addResource(image);
game.load(loader);

var sprite = new Sprite(image, 0, 0, 32, 32);
{% endhighlight %}


## Constructor 
<pre>new(image: PreloadedImage, public sx: number, public sy:number, public swidth: number, public sheight : number)</pre>
--------------

The Actor constructor takes 5 optional parameters, x position, y position,
width, height, and color. If no parameters are specified x, y, width, and 
height will all default to 0. Color will default to black.

## Properties
<pre>sprite.sx</pre>
-------------

Sets or gets the x coordinate of the sprite's source image.

<pre>sprite.sy</pre>
-------------

Sets or gets the y coordinate of the sprite's source image.

<pre>sprite.swidth</pre>
-------------

Sets or gets the width of the sprite in source image pixels.

<pre>sprite.sheight</pre>
-------------

Sets or gets the height of the sprite in source image pixels.

## Methods
<pre>sprite.draw(ctx: CanvasRenderingContext2D, x: number, y: number)</pre>
-------------

Draws the image to the game's graphics context at a specified x pixel coordinate
and a specified y pixel coordinate.