---
layout: docs
title: Logger
prev_section: label
next_section: color
permalink: /docs/log/
---

Excalibur comes with a logger in the same style as the log4j or log4net logging
tools. The logger in Excalibur is a singleton.

## Usage
--------
{% highlight javascript %}
var logger = Logger.getInstance();

logger.log("some message", Log.INFO);
{% endhighlight %}


## Properties
<pre>logger.defaultLevel</pre>
-------------

Gets or sets the default logging level of the logger to a specific value. If 
the defualt level is set to "WARN" then only warn level and above will be 
reported to the log.

## Static Methods
<pre>Logger.getInstance</pre>
-------------

Returns the current singleton instance of the logger.

## Methods
<pre>logger.log(message: string, level?: Log)</pre>
-------------

Log a message to the logger. If no level is specified the message will be 
logged at the default level.

<pre>logger.addAppender(appender : IAppender)</pre>
------------

Add a specific appender to the logger. By default, Excalibur comes with a 
"ConsoleAppender" and a "ScreenAppender". The "ConsoleAppender" writes logs
to the browser console and the "ScreenAppender" writes logs to the screen.
