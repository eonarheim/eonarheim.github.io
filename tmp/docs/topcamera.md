---
layout: docs
title: Top Camera
prev_section: sidecamera
next_section: point
permalink: /docs/topcamera/
---

The Top Camera is a top-down camera that follow the player horizontally
and vertically. This may be useful in games where the camera needs to be locked
to the center of the screen.

## Usage
--------
{% highlight javascript %}
var game = new ex.Engine();
var actor = new ex.Actor();

var camera = ex.TopCamera(game);
camera.setActorToFollow(actor);

game.camera = camera;
game.start();
{% endhighlight %}


## Constructor 
<pre>new(engine: ex.Engine)</pre>
--------------

The Top Camera constructor takes the game engine as a parameter.

## Methods
<pre>camera.getFocus(): e.Point</pre>
--------------

Returns a point representing the center of the camera's focus.

<pre>camera.applyTransform()</pre>
--------------

This method is called by the engine to translate the canvas to the
camera's focus. It **should not** be called by user code normally. 
