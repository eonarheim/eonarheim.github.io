---
layout: docs
title: Promises
prev_section: sound
next_section: loader
permalink: /docs/promises/
---

Excalibur implements promises following the Promises/A+ specification. Promises
are an incredibly useful tool for managing asynchronous behaviour in you game. A 
promise is a single-use object meant to capture asychronous behavior, like 
callbacks. Promises **should not** be used as an eventing system.

## Usage
--------
{% highlight javascript %}

var promise = new Promise();

promse.then(function(val){
	console.log("Promise was resolved with some value", val);
}).then(function(val){
	// somthing else 
}).then(function(val){
	// something else again
});

// Something async
setTimeout(function(){
	// Something interesting
	promise.resolve(Math.random());	
}, 3000);

{% endhighlight %}


## Constructor 
<pre>new<T>()</pre>
--------------

The Promise constructor takes no arguments. Promises are created in the default
pending state.

## Methods
<pre>promise.then(successCallback? : (value? : any) => any, rejectCallback? : (value? : any) => any) : IPromise</pre>
------------------

Registers the success callback and the reject callback with the promise. If 
the promise is resolved, then the success callback will be fired with the 
resolved value as an argument. If the promise is rejected, then the reject
callback will be fired with the rejected value as an argument.

<pre>promise.error(errorCallback? : (value? : any) => any) : IPromise</pre>
------------------

If either the resolve or reject callback throw an exception during their 
execution the error callback will be fired.

<pre>promise.resolve(value? : any) : IPromise</pre>
------------------

When a promise is resolved with a value, all success callbacks will be fired
in the order they were added.

<pre>promise.reject(value? : any) : IPromise</pre>
------------------

When a promise is rejected, the last rejected callback to be added will fired.


<pre>promise.state() : PromiseState;</pre>
------------------

Queries the current state of a promise. Valid states for a promise are 'pending',
'resolved', and 'rejected'.

{% highlight javascript %}
enum PromiseState {
   Resolved,
   Rejected,
   Pending,
}
{% endhighlight %}

## Static Methods

<pre>Promise.wrap(value? : any) : IPromise</pre>
------------------

Sometimes when working with promises, you want to wrap a value type inside of a
resolved promise. 
