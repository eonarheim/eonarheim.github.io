---
layout: docs
title: Actor
prev_section: engine
next_section: log
permalink: /docs/actor/
---

The most important primitive in Excalibur is an "Actor." Anything that can move on the
screen, collide with another Actor, respond to events, or interact with the current scene, 
must be an actor.

## Usage
--------
{% highlight javascript %}
var game = new Engine();

// Create new actor at x = 50, y = 50, width = 10, height = 10, and color = black
var actor = new Actor(50, 50, 10, 10, Color.fromHex('#000000'));

game.addChild(actor);

game.start();
{% endhighlight %}


## Constructor 
<pre>new(x? : number,  
   y? : number,  
   width? : number, 
   height? : number, 
   color? : Color)</pre>
--------------

The Actor constructor takes 5 optional parameters, x position, y position,
width, height, and color. If no parameters are specified x, y, width, and 
height will all default to 0. Color will default to black.

## Properties
<pre>actor.x</pre>
------------------

The x position of the actor in game coordinates. Defaults to 0.

<pre>actor.y</pre>
------------------

The y position of the actor in game coordinates. Defaults to 0.

<pre>actor.rotation</pre>
-------------------------

The current rotation of an actor in radians. Defaults to 0 radians.

<pre>actor.scale</pre>
----------------------

The current scale of an actor. Defaults to 1.

<pre>actor.dx</pre>
-------------------

The current x velocity of an actor. Defaults to 0.

<pre>actor.dy</pre>
-------------------

The current y velocity of an actor. Defaults to 0.

<pre>actor.rx</pre>
-------------------

The current angular velocity of an actor. Defaults to 0.

<pre>actor.sx</pre>
-------------------

The current scale velocity of an actor. Defaults to 0.

<pre>actor.invisible</pre>
-------------------

Get or set the current visibility of an actor. If invisible is set to
true then the actor will no longer be drawn, but will still receive 
updates.

<pre>actor.solid</pre>
-------------------

If 'solid' is set to true the actor will not be pushed by other actors
on collision. If 'solid' is set to false then other actors will influence
the current actors position on collision.

<pre>actor.frames</pre>
-------------------

Dictionary containing all the drawable images/animations for an actor. You 
*should not* be adding to this directory. Use the 'addDrawing' method below.

<pre>actor.currentDrawing</pre>
-------------------

The current drawing being displayed for this actor. You *should not* ever
set this property. Use the 'setDrawing' method below.

<pre>actor.color</pre>
-------------------

The current color for an actor, this is only used if no drawings have been
specified for an actor.

<pre>actor.parent</pre>
-------------------

The parent property represents the SceneNode that is this actors parent.
This property is null by default and is set when the actor is added to the
scene graph.

## Methods

<pre>actor.kill()</pre>
-------------------

This is a convenience method to remove the current actor from the scene. Actors
that are removed from the scene will no longer be drawn or updated. 

<pre>actor.addChild(actor : Actor)</pre>
-------------------

Adds a child actor to this actor. This allows you to move the parent actor
around and have children automatically follow.

*Note* All child coordinates are relative to the parent.

<pre>actor.removeChild(actor : Actor)</pre>
-------------------

Removes a child actor from this actor.

<pre>actor.addDrawing(key : string, drawing : Drawing.IDrawable)</pre>
-------------------

Adds a drawing to the collection of available drawings for an actor.

<pre>actor.setDrawing(key : string)</pre>
-------------------

Set the current drawing for the actor from the available drawing collection.

<pre>actor.addEventListener(eventName : string,  
   handler: (event?: ActorEvent) => void)</pre>
---------------------------

Add an event listener to this actor, you can listen for a variety of events 
off of the actor, see the events section below for a complete list.

<pre>actor.triggerEvent(eventName : string, event? : ActorEvent)</pre>
-------------------

Trigger an event to occur off of an actor.

<pre>actor.getCenter()</pre>
-------------------

Returns a vector with the x and y position of the center of the actor.

<pre>actor.getWidth()</pre>
-------------------

Returns the width of an actor factoring in the scale.

<pre>actor.setWidth(width : number)</pre>
-------------------

Sets the width of an actor factoring in the scale.


<pre>actor.getHeight()</pre>
-------------------

Returns the height of an actor factoring in the scale.


<pre>actor.setHeight(height : number)</pre>
-------------------

Sets the height of an actor factoring in the scale.

<pre>actor.getLeft()</pre>
-------------------

Returns the x position of the left side of the actor's bounding box.

<pre>actor.getRight()</pre>
-------------------

Returns the x position of the right side of the actor's bounding box.

<pre>actor.getTop()</pre>
-------------------

Returns the y position of the top side of the actor's bounding box.

<pre>actor.getBottom()</pre>
-------------------

Returns the y position of the bottom side of the actor's bounding box.

<pre>actor.contains(x : number, y : number)</pre>
-------------------

Returns true if the x and y position specified are inside or on the edge of
the actor's bounding box.

<pre>actor.collides(other : Actor)</pre>
-------------------

Returns the 'Side' of the other actor, if actor collides with the other actor. 
Otherwise it returns the 'None' side.

<pre>actor.within(other : actor, distance : number)</pre>
-------------------

Returns true if the two actors are less than or equal to the distance specified.

<pre>actor.moveTo(x : number, y : number, speed : number</pre>
-------------------

This method will move an actor to the specified x and y position at the speed
specified (in pixels per second) and return back the actor.

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.moveBy(x : number, y : number, time : number</pre>
-------------------

This method will move an actor to the specified x and y position by a certain
time (in milliseconds).

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.rotateTo(angleRadians : number, speed : number</pre>
-------------------

This method will rotate an actor to the specified angle at the speed
specified (in radians per second) and return back the actor.

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.rotateBy(angleRadians : number, time : number</pre>
-------------------

This method will rotate an actor to the specified angle by a certain time 
(in milliseconds) and return back the actor.

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.scaleTo(size : number, speed : number</pre>
-------------------

This method will scale an actor to the specified size at the speed
specified (in magnitude increase per second) and return back the actor.

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.scaleBy(size : number, time : number</pre>
-------------------

This method will scale an actor to the specified size by a certain time
(in milliseconds) and return back the actor.

This method is part of the actor 'Action' fluent api allowing action chaining. 


<pre>actor.blink(frequency : number, duration : number)</pre>
-------------------

This method will cause an actor to blink (become visible and and invisible) at
a frequency (blinks per second) for a duration (in milliseconds).

To have the actor blink 3 times in 1 second, call actor.blink(3, 1000).

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.delay(time : number)</pre>
-------------------

This method will delay the next action from executing for a certain amount of
time (in milliseconds).

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.repeat(times? : number)</pre>
-------------------

This method will cause the actor to repeat all of the previously called actions 
a certain number of times. If the number of repeats is not specified it will 
repeat forever.

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.repeatForever()</pre>
--------------------

This method will cause the actor to repeat all of the previously called actions
forever.

This method is part of the actor 'Action' fluent api allowing action chaining. 

<pre>actor.update(engine : Engine, delta : number)</pre>
--------------------

This method is called by the engine to update each actor. Delta is the amount
of time elapsed since the last time update was called (in milliseconds).

You should only be calling this method if you wish to extend actor.

<pre>actor.draw(ctx: CanvasRenderingContext2D, delta: number)</pre>
--------------------

This method is called by the engine to draw each actor. Delta is the amount
of time elapsed since the last time draw was called (in milliseconds).

You should only be calling this method if you wish to extend actor.


<pre>actor.debugDraw(ctx: CanvasRenderingContext2D)</pre>
--------------------

This method is called by the engine when in debug mode. This will add general
debug information to the screen.

## Events

Valid events to listen for off of Actor.

<pre>'keydown'</pre>
<pre>'keyup'</pre>
<pre>'keypressed'</pre>
<pre>'update'</pre>
<pre>'click'</pre>
<pre>'mousedown'</pre>
<pre>'mouseup'</pre>

See the events documentation for specifics about each of these events.
