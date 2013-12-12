---
layout: docs
title: Side Camera
prev_section: loader
next_section: topcamera
permalink: /docs/sidecamera/
---

The Side Camera is a side locked camera that follow the player horizontally. This
is useful for many side scrolling games.

## Usage
--------
{% highlight javascript %}
var game = new Engine();
var actor = new Actor();

var camera = Drawing.SideCamera(game);
camera.setActorToFollow(actor);

game.camera = camera;
game.start();
{% endhighlight %}


## Constructor 
<pre>new(engine : Engine)</pre>
--------------

The Side Camera constructor takes the game engine as a parameter.

## Methods
<pre>camera.getFocus() : Point</pre>
--------------

Returns a point representing the center of the camera's focus.

<pre>camera.applyTransform()</pre>
--------------

This method is called by the engine to translate the canvas to the
camera's focus. It **should not** be called by user code normally.