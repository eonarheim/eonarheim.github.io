---
layout: docs
title: Animation
prev_section: sprite
next_section: texture
permalink: /docs/animation/
---

Animations allow you to display a series of images one after another, creating
the illusion of change. Generally these images will come from a sprite 
sheet source.

## Usage
-----------
{% highlight javascript %}
// Load image into Excalibur
var game = new Engine();
var loader = new Loader();
var image = new Texture("myspritesheet.png");
loader.addResource(image);
game.load(loader);

// Create a spritesheet with the loaded image
var sprites = new Drawing.SpriteSheet(image, 10, 10, 32, 32);

// Create animation for indices 1,2, and 5 speeding 200 ms on each frame
var anim = sprites.getAnimationByIndices(game, [1,2,5], 200);

{% endhighlight %}

## Constructor
<pre>new(engine : Engine, images: Sprite[], speed: number, loop? : boolean)</pre>
-----------

The Animation constructor takes the game engine, a list of images (Sprites),
the speed for each frame, and whether or not the animation loops.


## Properties
<pre>animation.loop</pre>
-----------

Gets or sets the looping property on animations. Setting this property to true
will cause the animation to loop forever.

## Methods
<pre>animation.setRotation(radians: number)</pre>
-----------

Sets the rotation of the animation by a certain angle (in radians).

<pre>animation.setScale(scale: number)</pre>
-----------

Set the scale of the animation by an amount (for example, setting this to 2 would double 
the size of the animation).

<pre>animation.reset()</pre>
-----------

Rewinds the animation back to the first frame.

<pre>animation.isDone()</pre>
-----------

If animation.loop is set to false, isDone() will return true after the last
frame of the animation has been played.

<pre>animation.tick()</pre>
-----------

Tick potentially advances the frame of the animation, this method is called by 
Excalibur. You **should not** call tick.

<pre>animation.draw(ctx: CanvasRenderingContext2D, x: number, y: number)</pre>
-----------

Draw will draw the current frame of the animtaion onto the graphics 
context at a certain x and y.

<pre>animation.play (x : number, y : number)</pre>
-----------

This will play the animation at any arbitrary x and y location in the game. 
This is useful for animations not strictly tied to actors, like explosions.

