---
layout: docs
title: Basic Actions
prev_section: Loader
next_section: sidecamera
permalink: /docs/actions/
---

Actions are a special type of method on actors that allow motions to be scripted. 
Actions operate in a "fluent" style allowing you to chain actions together.
These are incredibly useful when creating NPCs (non player characters), scripted
cinematics, and AIs.

A platformer with moving platforms is a good example of how you might use the moveTo 
and repeatForever actions. 
<div class="align-center">
   <img class="border" src="/img/PlatformAction.gif">
</div>

{% highlight javascript %}
var game = new Engine();

// Create an actor to be our platform
var platform = new Actor(50, 50, 100, 20, Color.Azure);

// Move the actor to (150, 50) moving at 50 pixels per second, then
// move back to (50, 50) moving at 50 pixels per second, finally
// repeate the previous two forever.
platform.moveTo(150, 50, 50).moveTo(50, 50, 50).repeatForever();

game.addChild(platform);
game.start();

{% endhighlight %}

