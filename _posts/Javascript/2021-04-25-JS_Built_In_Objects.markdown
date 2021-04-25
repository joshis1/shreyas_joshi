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

There are certain in built methods that are very much important in order to transform the format from string to a number.

{% highlight ruby %}

var a = '5';
console.log(a); // "5"
console.log(parseInt(a)); //5

var a = 'test';
console.log(parseInt(a)); // NaN

var a = 'FB123';
console.log(parseInt(a)); //NaN
console.log(parseInt(a,16)); //1028387

var a = 10;
console.log(a.toString()); // '10'

var a = 10.3;
console.log(a.toFixed()); // 10

console.log(a.toFixed(2)); //10.30

{% endhighlight %}

**string functions**

string is nothing but an array of characters. In short, string can be treated like an array i.e. we can use subscript to access a particular element in a string. Here is an example.
Please note that string is immutable therefore when you do operations on a string then it won't modify the existing string but it will return another string.

{% highlight ruby %}
  var string = 'Any text';
  console.log(string);

  console.log(string.length); //8
  console.log(string[2]); //'y'

  console.log(string.charAt(2)); //'y'

  var newString  = string.concat(' add new string');

  console.log(newString); //"Any text add new string"

  var uppString = string.toUpperCase();
  console.log(uppString); //"ANY TEXT"

  var lowString = string.toLowerCase();
  console.log(lowString); //"any text"

  var splitString = string.split(' ');
  console.log(splitString); //["Any", "text"]
  console.log(splitString[0]); //"Any"
  console.log(splitString[1]); //"text"

  var userString = ' Any text ';
  console.log(userString); //" Any text "
  // all the heading and trailing white spaces will be removed when used trim
  console.log(userString.trim()); //"Any text"

  console.log(string); //"Any text"

{% endhighlight %}

References - 

https://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind#:~:text=Call%20invokes%20the%20function%20and,and%20any%20number%20of%20arguments. 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind 

https://jsbin.com/vomadedive/edit?html,js,console,output 