---
layout: docs
title: Sound
prev_section: texture
next_section: promises
permalink: /docs/sound/
---

The Sound object allows games built in Excalibur to have basic audio components,
from soundtracks to sound effects. It is generally recommended to preload 
sound using the "Sound" object.

## Usage
--------
{% highlight javascript %}
// Load sound into Excalibur
var game = new ex.Engine();
var loader = new ex.Loader();
var sound = new ex.Sound("awesometrack.mp3", "awesometrackfallback.wav");
loader.addResource(sound);
game.start(loader).then(()=>{
   // Play the sound after it has
   sound.play();   
});
{% endhighlight %}


## Constructor 
<pre>new(...paths : string[])</pre>
--------------

The Sound constructor takes a list of paths and will load the appropriate audio for the browser, with file paths on the left taking preference. If your browser does not support any of the file types, Excalibur will attempt to load the first audio file.

## Methods
<pre>sound.setVolume(volume : number)</pre>
--------------

Sets the volume that the sound will play at between 0-1. 0 begin silent, and
1 being full volume.


<pre>sound.setLoop(loop : boolean)</pre>
--------------

Sets the looping property. If set to true, the sound will loop forever.

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
