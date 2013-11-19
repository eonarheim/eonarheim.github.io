---
layout: docs
title: Images
prev_section: animation
next_section: sound
permalink: /docs/image/
---

The Image object allows games built in Excalibur to load image resources.
It is generally recommended to preload images using the "PreloadedImage" object.

## Usage
--------
{% highlight javascript %}
// Load image into Excalibur
var game = new Engine();
var loader = new Loader();
var image = new PreloadedImage("someimage.png");
loader.addResource(image);
game.load(loader);
{% endhighlight %}

## Constructor 
<pre>new(path : string)</pre>
--------------

The Image constructor takes a path to an audio file.

## Properties
<pre>image.image : HTMLImageElement</pre>

Gets the internal HTMLImageElement once the image has been loaded.

## Methods

<pre>load() : Promise<HTMLImageElement></pre>
--------------

Begins loading the image and returns a promise that will be resolved when
loading is complete.
