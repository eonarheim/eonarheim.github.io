---
layout: docs
title: Sound
prev_section: animation
next_section: none
permalink: /docs/sound/
---

The Sound object allows games built in Excalibur to have basic audio components,
from sound tracks to sound effects. It is generally recommended to preload 
sound using the "PreloadedSound" object.

## Usage
--------
{% highlight javascript %}
// Load sound into Excalibur
var game = new Engine();
var loader = new Loader();
var sound = new PreloadedSound("awesometrack.mp3");
loader.addResource(sound);
game.load(loader);


// Play the sound
sound.play();

{% endhighlight %}


## Constructor 
<pre>new(path : string, volume? : number)</pre>
--------------

The Sound constructor takes a path to an audio file, and optionally a value 
between 0-1. If no volume is specified the default volume is 1.

## Methods
<pre>sound.setVolume(volume : number)</pre>
--------------

Sets the volume that the sound will play at between 0-1. 0 begin silent, and
1 being full volume.


<pre>sound.setLoop(loop : boolean)</pre>
--------------

Sets the looping property, if set to true the sound will loop forever.

<pre>sound.load()</pre>
--------------

Loads the sound into memory. Sounds **must** be loaded into memory before
they can be played. It is recommeded that you use the "PreloadedSound" 
object to do this.

<pre>sound.play()</pre>
-------------

Begins playing the sound until it is completed or stopped.

<pre>sound.stop()</pre>
------------

If this sound is playing, this method stops playback.
