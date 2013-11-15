---
layout: docs
title: Installation
prev_section: home
next_section: quickstart
permalink: docs/install/
---

Excalibur is really easy to include into your project.

## Installing Excalibur

There are a few ways to install Excalibur the first is to download the 
source and include it in your page. Like so

{% highlight html %}
<script type="text/javascript" src="/path/to/Excalibur.js"></script>
<script type="text/javascript">
   // TODO: Build an awesome game
</script>

{% endhighlight %}

Or, if you like TypeScript just include a reference to the Excalibur 
declarations file in your root TypeScript file. Now you have a strongly
typed version of Excalibur.

{% highlight javascript %}
/// <reference path="/path/to/Excalibur.d.ts" />
var game : Engine = new Engine();
{% endhighlight %}

