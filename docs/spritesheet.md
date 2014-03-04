---
layout: docs
title: SpriteSheet
prev_section: color
next_section: sprite
permalink: /docs/spritesheet/
---

The "SpriteSheet" object allows you to use multiple images at the same time. Sprite sheets 
allow you to compact all of the images and animations in your game into a single image.

## Usage
--------
{% highlight javascript %}
// Load image into Excalibur
var game = new ex.Engine();
var loader = new ex.Loader();
var image = new ex.Texture("myspritesheet.png");
loader.addResource(image);

// Create a spritesheet with the loaded image
var sprites = new ex.SpriteSheet(image, 10, 10, 32, 32);

game.start(loader);

{% endhighlight %}


## Constructor 
<pre>new(public image : Texture, private columns: number, private rows: number, spWidth: number, spHeight: number)</pre>
--------------

The SpriteSheet constructor takes a preloaded image argument, the number of 
columns of images in your sprite sheet, the number of rows of images in your sprite
sheet, the width in pixels of each individual sprite, and the height in pixels
of each individual sprite.

## Properties
<pre>spriteSheet.image</pre>
-------------

Gets the internal preloaded image.

<pre>spriteSheet.sprites</pre>
-------------

Gets or sets the list of individul sprites.

## Methods
<pre>spriteSheet.getAnimationByIndices(engine: ex.Engine, indices: number[], speed: number)</pre>
--------------

Returns an "Animation" by specifying the engine, the indices of each sprite in 
the animation, and the speed (in milliseconds) that each frame should take in the 
animation. Sprites in the sprite sheet are indexed in row-major order, meaning 
that each sprite is numbered starting at zero beginning at the first row, then at zero at 
the second row, etc.

<pre>spriteSheet.getAnimationBetween(engine: ex.Engine, beginIndex: number, endIndex: number, speed: number)</pre>
--------------

Returns an "Animation" by specifying a beginning sprite index (inclusive) and 
an end sprite index (exclusive), and a speed for each frame. Indices are 
specified in row-major order.

<pre>getAnimationForAll(engine: ex.Engine, speed: number)</pre>
---------------

Returns an "Animation", treating every sprite in the sprite sheet as members of the 
animation.

<pre>getSprite(index: number)</pre>
--------------

Returns a "Sprite" at a specific index in the sprite sheet (in row-major order).
