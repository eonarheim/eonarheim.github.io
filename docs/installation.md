---
layout: docs
title: Installation
prev_section: home
next_section: quickstart
permalink: docs/install/
---

Excalibur is very easy to include into your project.

## Installing Excalibur

There are a few ways to install Excalibur. The first is to [download the 
source](https://github.com/eonarheim/Excalibur/releases/) and include at **the bottom** of 
the body tag.

{% highlight html %}
<html>
<head></head>   
<body>
<!-- Other stuff -->

   <script type="text/javascript" src="/path/to/Excalibur.js"></script>
   <script type="text/javascript">
      // TODO: Build an awesome game in JavaScript here
   </script>
</body>
</html>

{% endhighlight %}

If you are using TypeScript, just include a reference to the Excalibur 
declarations file in your root TypeScript file. Now you have a strongly
typed version of Excalibur.

{% highlight javascript %}
/// <reference path="/path/to/Excalibur.d.ts" />
var game : Engine = new ex.Engine();
// TODO: Build an awesome game in TypeScript here
{% endhighlight %}

## Nuget Support

We are currently in the Nuget.org package library as an alpha package. You can run
the command
{% highlight rconsole %}
PM> Install-Package Excalibur -Pre
{% endhighlight %}

Or find us in the VS Nuget Package Manager with "Include Prelease" turned on.


