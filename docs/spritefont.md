---
layout: docs
title: SpriteFont
prev_section: sprite
next_section: animation
permalink: /docs/Spritefont/
---

A SpriteFont is just an image that represents a some font as an image. SpriteFonts
can be used to add more variety to the fonts in your game.

## Usage
--------
{% highlight javascript %}
// Load image into Excalibur
var game = new Engine();
var loader = new Loader();
var image = new Texture("spriteFont.png");
loader.addResource(image);
game.load(loader);

var spriteFont = new new Drawing.SpriteFont(spriteFontImage, '0123456789abcdefghijklmnopqrstuvwxyz,!\'&."?- ', true, 16, 3, 16, 16);

var label = Label("Some Text", spriteFont);
{% endhighlight %}


## Constructor 
<pre>new(public image : Texture, 
   private alphabet : string, 
   private caseInsensitive : boolean, 
   columns : number, 
   rows : number, 
   spWidth : number, 
   spHeight : number)</pre>
--------------

The SpriteFont constructor takes 6 arguments. The first being the loaded 
"Texture" resourse that contains the font. The next argument specifies the 
alphabet of the font in row major order. Additionally the number of columns,
rows, and the height and width of each individual sprite are required.

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