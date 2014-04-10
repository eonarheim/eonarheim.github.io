---
layout: docs
title: Basic Actions
prev_section: Loader
next_section: sidecamera
permalink: /docs/actions/
---

Actions are a special type of method on actors that allow motions to be scripted. 
Actions operate in a "fluent" style allowing you to chain actions together.
They are incredibly useful when creating NPCs (non player characters), scripted
cinematics, and AIs.

A platformer with moving platforms is a good example of how you might use the moveTo 
and repeatForever actions. 
<div class="align-center">
   <img class="border" src="/img/PlatformAction.gif">
</div>

{% highlight javascript %}
var game = new ex.Engine();

// Create an actor to be our platform
var platform = new ex.Actor(50, 50, 100, 20, ex.Color.Azure);

// Move the actor to (150, 50) moving at 50 pixels per second, then
// move back to (50, 50) moving at 50 pixels per second, finally
// repeate the previous two forever.
platform.moveTo(150, 50, 50).moveTo(50, 50, 50).repeatForever();

game.addChild(platform);
game.start();

{% endhighlight %}


<pre>actor.moveTo(x: number, y: number, speed: number</pre>
-------------------

This method will move an actor to the specified x and y position at the speed
specified (in pixels per second) and return back the actor.

This method is part of the actor 'Action' fluent API allowing action chaining. 

<pre>actor.moveBy(x: number, y: number, time: number</pre>
-------------------

This method will move an actor to the specified x and y position by a certain
time (in milliseconds).

This method is part of the actor 'Action' fluent API allowing action chaining. 

<pre>actor.rotateTo(angleRadians: number, speed: number</pre>
-------------------

This method will rotate an actor to the specified angle at the speed
specified (in radians per second) and return back the actor.

This method is part of the actor 'Action' fluent API allowing action chaining. 

<pre>actor.rotateBy(angleRadians: number, time: number</pre>
-------------------

This method will rotate an actor to the specified angle by a certain time 
(in milliseconds) and return back the actor.

This method is part of the actor 'Action' fluent API allowing action chaining. 

<pre>actor.scaleTo(size: number, speed: number</pre>
-------------------

This method will scale an actor to the specified size at the speed
specified (in magnitude increase per second) and return back the actor.

This method is part of the actor 'Action' fluent API allowing action chaining. 

<pre>actor.scaleBy(size: number, time: number</pre>
-------------------

This method will scale an actor to the specified size by a certain time
(in milliseconds) and return back the actor.

This method is part of the actor 'Action' fluent API allowing action chaining. 


<pre>actor.blink(frequency: number, duration: number, blinkTime? number)</pre>
-------------------

This method will cause an actor to blink (become visible and and invisible) at
a frequency (blinks per second) for a duration (in milliseconds). Optionally, you
may specify blinkTime, which indicates the amount of time the actor is invisible
during each blink.

To have the actor blink 3 times in 1 second, call actor.blink(3, 1000).

This method is part of the actor 'Action' fluent API allowing action chaining. 

<pre>actor.delay(time: number)</pre>
-------------------

This method will delay the next action from executing for a certain amount of
time (in milliseconds).

This method is part of the actor 'Action' fluent API allowing action chaining. 

<pre>actor.repeat(times?: number)</pre>
-------------------

This method will cause the actor to repeat all of the previously called actions 
a certain number of times. If the number of repeats is not specified it will 
repeat forever.

This method is part of the actor 'Action' fluent API allowing action chaining. 

<pre>actor.repeatForever()</pre>
--------------------

This method will cause the actor to repeat all of the previously called actions
forever.

This method is part of the actor 'Action' fluent API allowing action chaining. 
