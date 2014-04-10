---
layout: docs
title: Label
prev_section: actor
next_section: log
permalink: /docs/label/
---

Labels are a special type of actor meant to be a convenient way to display text
on the screen. As a consequence of being an actor, all of the capabilities of
actors can be applied to a label.

## Usage
--------
{% highlight javascript %}
var game = new ex.Engine();

// Create new lable at x = 50, y = 50, with the text Hello World
var label = new ex.Label("Hello World", 100, 100);

game.addChild(label);

game.start();
{% endhighlight %}


## Constructor 
<pre>new(text?: string, x?: number, y?: number, font?: string, spriteFont?: ex.SpriteFont)</pre>
--------------

The Label constructor takes 4 optional arguments: the text to display, x 
coordinate, y coordinate, a font, and an optional SpriteFont. If a SpriteFont is specified, 
it will take precedence over the built-in font.

## Properties
<pre>label.text</pre>
------------------

The text to be drawn when the label is drawn. Defaults to empty string.

<pre>label.font</pre>
------------------

The built-in font to use when drawing the label.

<pre>label.spriteFont</pre>
------------------

The spriteFont associated with the text, if one has been set. Defaults to null.

## Methods

<pre>label.update(engine: ex.Engine, delta: number)</pre>
--------------------

This method is called by the engine to update each label. Delta is the amount
of time elapsed since the last time update was called (in milliseconds).

You should only be calling this method if you wish to extend label.

<pre>label.draw(ctx: CanvasRenderingContext2D, delta: number)</pre>
--------------------

This method is called by the engine to draw each label. Delta is the amount
of time elapsed since the last time draw was called (in milliseconds).

You should only be calling this method if you wish to extend label.


<pre>label.debugDraw(ctx: CanvasRenderingContext2D)</pre>
--------------------

This method is called by the engine when in debug mode. This will add general
debug information to the screen.

## Events

Valid events to listen for off of Label.

<pre>'keydown'</pre>
<pre>'keyup'</pre>
<pre>'keypressed'</pre>
<pre>'update'</pre>
<pre>'click'</pre>
<pre>'mousedown'</pre>
<pre>'mouseup'</pre>

See the events documentation for specifics about each of these events.
