---
layout: docs
title: Loader
prev_section: actor
next_section: none
permalink: /docs/loader/
---

The loader provides a mechanism to preload multiple resources at one time. The 
loader must be passed to the engine in order to trigger the loading progress
bar.

## Usage
--------
{% highlight javascript %}
// Load resources into Excalibur
var game = new Engine();
var loader = new Loader();
var sound = new Sound("awesometrack.mp3");
var image = new Texture("awesomeimage.png");
loader.addResources([sound, image]);

// Initiate load
// You must load resources before use!
game.load(loader);

{% endhighlight %}


## Constructor 
<pre>new(loadables? : ILoadable[])</pre>
--------------

The Loader constructor takes an optional list of loadables. The loader can
be initialize with other methods as well.

## Methods
<pre>loader.addResource(loadable : ILoadable)</pre>
--------------

Add a single resource to be loaded to the loader's collection.

<pre>loader.addResources(loadables : ILoadable[])</pre>
--------------

Add mulitiple resources to be loaded to the loader's collection.

<pre>loader.load() : Promise<any></pre>
--------------

Begins loading all of the resources that have been added to the loader. Returns
a promise that will resolve when loading is complete.
