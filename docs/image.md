---
layout: docs
title: Texture
prev_section: animation
next_section: sound
permalink: /docs/texture/
---

The Texture object allows games built in Excalibur to load image resources.
It is generally recommended to preload images using the "Texture" object.

## Usage
--------
{% highlight javascript %}
// Load image into Excalibur
var game = new ex.Engine();
var loader = new ex.Loader();
var texture = new ex.Texture("someimage.png");
loader.addResource(texture);

game.start(loader);
{% endhighlight %}

## Constructor 
<pre>new(path: string)</pre>
--------------

The Texture constructor takes a path to an audio file.

## Properties
<pre>texture.image: HTMLImageElement</pre>

Gets the internal HTMLImageElement once the image has been loaded.

## Methods

<pre>load(): ex.Promise<HTMLImageElement></pre>
--------------

Begins loading the image and returns a promise that will be resolved when
loading is complete.
