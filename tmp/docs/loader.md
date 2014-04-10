---
layout: docs
title: Loader
prev_section: promises
next_section: actions
permalink: /docs/loader/
---

The loader provides a mechanism to preload multiple resources at one time. The 
loader must be passed to the engine in order to trigger the loading progress
bar.

## Usage
--------
{% highlight javascript %}
// Load resources into Excalibur
var game = new ex.Engine();
var loader = new ex.Loader();
var sound = new ex.Sound("awesometrack.mp3", "awesometrackfallback.wav");
var image = new ex.Texture("awesomeimage.png");
loader.addResources([sound, image]);


// or initiate load on game start
game.start(loader);

{% endhighlight %}


## Constructor 
<pre>new(loadables?: ex.ILoadable[])</pre>
--------------

The Loader constructor takes an optional list of loadables. The loader can
be initialized with other methods as well.

## Methods
<pre>loader.addResource(loadable: ex.ILoadable)</pre>
--------------

Add a single resource to be loaded to the loader's collection.

<pre>loader.addResources(loadables: ex.ILoadable[])</pre>
--------------

Add mulitiple resources to be loaded to the loader's collection.

<pre>loader.load(): ex.Promise<any></pre>
--------------

Begins loading all of the resources that have been added to the loader. Returns
a promise that will resolve when loading is complete.
