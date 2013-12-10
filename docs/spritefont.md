---
layout: docs
title: SpriteFont
prev_section: sprite
next_section: animation
permalink: /docs/Spritefont/
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
var image = new PreloadedImage("spriteFont.png");
loader.addResource(image);
game.load(loader);

var spriteFont = new new Drawing.SpriteFont(spriteFontImage, '0123456789abcdefghijklmnopqrstuvwxyz,!\'&."?- ', true, 16, 3, 16, 16);
{% endhighlight %}


## Constructor 
<pre>new(public image : PreloadedImage, 
   private alphabet : string, 
   private caseInsensitive : boolean, 
   columns : number, 
   rows : number, 
   spWidth : number, 
   spHeight : number)</pre>
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
<pre>sprite.draw(ctx: CanvasRenderin