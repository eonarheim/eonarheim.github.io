---
layout: docs
title: Engine
next_section: actor
permalink: /docs/engine/
---

The 'Engine' object is the main driver for a game. It is responsible for 
starting/stopping the game, maintaining state, transmitting events, 
loading resources, and managing the scene.

## Usage
--------
{% highlight javascript %}

var game = new Engine(600, 400, 'my-game');
// TODO: Build game
game.start();

{% endhighlight %}


## Constructor 
<pre>new(width? : number, height? : number, canvasElementId? : string,  displayMode? : DisplayMode)</pre>
--------------

The Engine constructor takes 4 optional parameters, a game width, height, 
a target canvas element to draw to, and a display mode. If the 'canvasElementId'
is not specified a new canvas will be appended to the body of the page and
the game will be drawn to that. If the 'displayMode' is not specified then the
default displayMode will be FullScreen.

## Properties

<pre>engine.canvas</pre>
------------------------

Reference to the current html canvas element the game is drawing to.

<pre>engine.ctx</pre>
---------------------

Reference to the current html canvas rendering context. This may be used to 
implement custom drawing methods for extended actors.

<pre>engine.backgroundColor</pre>
---------------------

Gets or sets the background color of the game.

<pre>engine.displayMode</pre>
---------------------

Gets the current display mode of the game. By default the displayMode 
defaults to FullScreen.

The Engine has 3 possible display modes:
{% highlight javascript%}
enum DisplayMode {
   FullScreen,
   Container,
   Fixed
}
{% endhighlight %}

**FullScreen** will force the engine to take up the entire screen.

**Container** will force the engine's canvas to fill up the size of its parent container.

**Fixed** will force the engine's canvas to take up a fixed height and width.


<pre>engine.isDebug</pre>
---------------------
Gets or sets the current debug mode. If 'isDebug' is set to true, debug information
will be drawn to the screen.

<pre>engine.width</pre>
-----------------------

The current width of the game's drawing surface in pixels.

<pre>engine.height</pre>
------------------------

The current height of the game's drawing surface in pixels.

<pre>engine.keys</pre>
----------------------

The list of currently pressed keys is available to you here. You **should** 
instead use the 'engine.isKeyPressed' method to detect specific key presses.


<pre>engine.keysUp</pre>
------------------------

The list of keys that received the 'keyup' event this frame. You **should**
instead use the 'engine.isKeyUp' method to detect specific key ups.

<pre>engine.keysDown</pre>
--------------------------

The list of keys that received the 'keydown' event this frame. You **should**
instead use the 'engine.isKeyDown' method to detect specific key downs.

<pre>engine.camera</pre>
------------------------

With the 'camera' property you can either get or set the current camera for the
game. By default there is no camera set and the property is 'null'. If you wish
to create a camera see the Camera documentation.

<pre>engine.currentScene</pre>
------------------------------

Access the current scene that is being drawn in the scene graph. To learn more
about scenes visit the Scene documentation.

<pre>engine.rootScene</pre>
---------------------------

Access the root scene in the scene graph. To learn more about scenes visit the
Scene documentation.

## Methods

<pre>engine.addEventListener(eventName : string,  
   handler: (event?: ActorEvent) => void)</pre>
---------------------------

Add an event listener to the engine, you can listen for a variety of events 
off of the engine, see the events section below for a complete list.

<pre>engine.setAntialiasing(isSmooth : boolean)</pre>
--------------------------

If supported by the browser, this will set the antialiasing flag on the canvas. 
Set this to false if you want a 'jaggy' pixel art look to your image resources.

<pre>engine.getAntialiasing() : boolean</pre>
--------------------------

If supported by the browser, this will return the current state of the 
antialiasing flag.

<pre>engine.playAnimation(animation : Drawing.Animation, 
   x : number, y : number)</pre>
--------------------------

Plays a sprite animation on the screen a specified x and y (in game 
coordinates, not screen pixels). These animations play independent of actors,
and will be cleaned up internally as soon as they are complete. *Note* animations
that loop will never be cleaned up.

<pre>engine.addChild(actor : Actor)</pre>
--------------------------

Adds an actor to the current scene of the game. This is synonymous to calling
engine.currentScene.addChild(actor : Actor). 

Actors can only be draw if they are a member of a scene, and only the 
'currentScene' may be drawn or updated.

<pre>engine.removeChild(actor : Actor)</pre>
--------------------------

Removes an actor from the currentScene of the game. This is synonymous to
calling engine.currentScene.removeChild(actor : Actor).

Actors that are removed from a scene will no longer be drawn or updated.

<pre>engine.pushScene(scene : SceneNode)</pre>
--------------------------

Pushes a new scene onto Excalibur's internal scene stack, and begins updating 
and drawing the top scene. This is useful if you need to change levels or screens.

<pre>engine.popScene()</pre>
--------------------------

This pops the current scene off of Excalibur's internal scene stack, returning
the game to the previous level or screen. The root scene can never be popped,
there will always be at least one scene in the game.

<pre>engine.isKeyUp(key : Keys) : boolean</pre>
---------------------------

Returns true if the 'key' parameter has received the 'keyup' event this frame.

<pre>engine.isKeyDown(key : Keys) : boolean</pre>
---------------------------

Returns true if the 'key' parameter has received the 'keydown' event this frame.

<pre>engine.isKeyPressed(key : Keys) : boolean</pre>
---------------------------

Returns true if the 'key' parameter is currently being pressed.

<pre>engine.start()</pre>
---------------------------

This must be called to start the game. This method initiates the internal 
mainloop.

<pre>engine.stop()</pre>
---------------------------

This pauses the game by stopping the engine's internal mainloop. This is 
useful when building pause game functionality. 

*Note* game events will no longer be sent, because the game is now paused.
The will be added to the queue and fired when the game is started again.

<pre>engine.load(loader : ILoadable) : Promise<any></pre>
----------------------------

Call load to prepare and image or sound assets in your game. This *must* be 
called before attempting to use images or sounds *anywhere*. Returns a [promise](/docs/promises)
that will be resolved when loading is complete.

<pre>engine.setLoadingDrawFunction (fcn : (ctx : CanvasRenderingContext2D,
 loaded : number, 
 total : number) => void)</pre>
----------------------------

Set a custom load screen to be drawn instead of the default asset loading
screen.


## Events

Valid events to listen for off of Engine.

<pre>'keydown'</pre>
<pre>'keyup'</pre>
<pre>'keypressed'</pre>
<pre>'update'</pre>
<pre>'click'</pre>
<pre>'mousedown'</pre>
<pre>'mouseup'</pre>

See the events documentation for specifics about each of these events.
