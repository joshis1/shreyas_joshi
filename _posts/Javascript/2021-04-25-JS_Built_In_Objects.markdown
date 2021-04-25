---
layout: post
title:  "Javascript built in Objects"
date:   2021-04-25 14:13:31 +1300
categories: Javascript
---

This article is all about javascript built in objects. In this article, we will discuss about some built in object methods like setTimeout(), setInterval(), transforming format and values, string functions.

**setTimeout**

The setTimeout() is a built in method that allows to run a function after a certain interval of time in millisconds.
Here is an example. In this example, after 2 seconds it will execute console.log function i.e. Hello. This can be used to create an animation i.e. fetch some code after some specific time has elapsed.

{% highlight ruby %}

setTimeout(function(){
  console.log('Hello');
}, 2000); //after 2 seconds, we see Hello

{% endhighlight %}

**setInterval**

Just like a timer, this will keep executing the given function at the interval specified in this method. Here is an example. In the example below, we will see ping every half a second. 

{% highlight ruby %}

 setInterval(function() {
    console.log('ping');
 }, 500);

{% endhighlight %}

**Stopping the timer**

The setInterval() once started will keep executing forever. However, there is a way to stop it. You can stop it using clearInterval(). For example, you want the setInterval to stop executing the timer after 5 seconds, then you could do so using setTimeout(). Here is an example to show this. In the example below, you will see Ping four times.

{% highlight ruby %}

 var interval = setInterval(function() {
    console.log('Ping');
 }, 500);

 setTimeout(function(){
   clearInterval(interval);
 }, 2000);

{% endhighlight %}

**Transforming format and Values**



References - 

https://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind#:~:text=Call%20invokes%20the%20function%20and,and%20any%20number%20of%20arguments. 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind 

https://jsbin.com/vomadedive/edit?html,js,console,output 