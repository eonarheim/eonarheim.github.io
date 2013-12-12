---
layout: docs
title: Quick Start
prev_section: install
next_section: engine
permalink: docs/quickstart/
---

Building a game is pretty simple, lets look at the "Hello World" example.



First [download](https://github.com/eonarheim/Excalibur/releases/), and include the Excalibur script at the bottom of the body tag:

{% highlight html %}
<script type="text/javascript" src="Excalibur.js"></script>
{% endhighlight %}

Then create the game container with the "Engine" constructor. The game container 
is responsible for running the mainloop that drives the game, maintaining the 
scene graph, and keeping track of all of the basic state related to the game.

It is important to call "game.start()" after you are finished building the game
to start the game.

{% highlight javascript %}
var game = new Engine();
// TODO: Setup game in here
game.start();
{% endhighlight %}

The most important primitive in Excalibur is an "Actor." Anything that can move on the
screen, collide with another actor, respond to events, or interact with the current scene, 
must be an actor.

In order for actors to take part in the game, they must be added to the game's current 
scene.

{% highlight javascript %}
var game = new Engine();

// Actor(x : number, y : number, w : number, h : number, color? : Color);
var actor = new Actor(20, 20, 100, 100, Color.Red);

// Add an actor to the current scene
game.addChild(actor);

// Start the game
game.start();
{% endhighlight %}


Right now our example game is pretty boring; we would like to have actors respond to user key
presses. We can accomplish this by adding event listeners to the actor for specific keys.
In Excalibur, you can listen for the "keypressed" event; however, there is a shorthand
for specific keys by just specifying the key in the "addEventListener" call.

{% highlight javascript %}
var game = new Engine();

// Actor(x : number, y : number, w : number, h : number, color? : Color);
var actor = new Actor(20, 20, 100, 100, Color.Red);

actor.addEventListener('up', function(){
   actor.y -= 10;
});

actor.addEventListener('down', function(){
   actor.y += 10;
});

actor.addEventListener('left', function(){
   actor.x -= 10;
});

actor.addEventListener('right', function(){
   actor.y += 10;
});

// Add an actor to the current scene
game.addChild(actor);

// Start the game
game.start();
{% endhighlight %}

Now we have a very simple game with rectangles responding to user
input.

**Note:** Generally it is a good idea to break each component of your game into 
separate files instead of building everything in your main file. Your main file
should be where the final assembly of your game happens.
