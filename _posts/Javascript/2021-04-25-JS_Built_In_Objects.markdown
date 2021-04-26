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

**Math Objects**

Math object provides a lot of built in methods and properties. Here is a list of such properties and methods.

{% highlight ruby %}

  var pi = Math.PI; 
  console.log(pi); //3.141592653589793

  var e = Math.E;
  console.log(e); //2.718281828459045

  var a = -3;
  console.log(Math.abs(a)); //3

  var a = 1.27;
  console.log(Math.round(a)); //1

  console.log(Math.ceil(a)); //2
  console.log(Math.floor(a)); //1

  var a = 2;
  console.log(Math.exp(a)); //7.38905609893065 nothing but e^2

  var e = Math.E;
  console.log(Math.log(e)); //1

  console.log(Math.max(1, 100, 1000)); //1000

  console.log(Math.min(1,100,1000)); // 1
  console.log(Math.random()); //any floating poing with 0.00x 
  var rand = Math.random() * 100;
  console.log(rand); // some floating point
  var rand1 = Math.floor(rand);
  console.log(rand1); // now random integer ranging from 0 to 100.
  // let's say we want from 1 to 101 any random then add 1 to it.
  console.log(rand1 + 1);

{% endhighlight %}

**Date Object**

The date object has a lot of built in methods. You could refer Date MDN javascript documentation to get more information. Here are some of the list.

{% highlight ruby %}

  var today = new Date();
  console.log(today); //gets an object
  console.log(today.toString()); //"Mon Apr 26 2021 08:25:13 GMT+1000 (Australian Eastern Standard Time)"

  //with numbers, the month is starting from 0 rather than 1. Thus 0 is January.
  var today = new Date(2021, 03, 30);
  console.log(today.toString()); //
"Fri Apr 30 2021 00:00:00 GMT+1000 (Australian Eastern Standard Time)"

// with string format, it can parse 5 as May only
 var today = new Date('2021/05/1');
 console.log(today.toString()); //"Sat May 01 2021 00:00:00 GMT+1000 (Australian Eastern Standard Time)"

  //parse gives number of milliseconds elapsed since January 1970 to this date.
 console.log(Date.parse('2021/05/1')); //
1619791200000

var today = new Date();
console.log(today.getDate()); //26

// the weekday in js starts from Sunday i.e. 0
// today is Monday therefore 1.
console.log(today.getDay()); //1

{% endhighlight %}

**Regular expression**

A regular expression pattern is expressed in javascript using / /. Just like string is expressed in ' ', a regular expression pattern is expressed as / /. The regular expression is nothing but an object. You can use exec() method of a regular expression object in order to do pattern matching on a string. Otherwise, you can use match() method of a string to do pattern matching. Here is an example.

{% highlight ruby %}

var s = 'abc';
var patt = /ab/;
var s1 = 'test';

console.log(patt.exec(s)); //["ab"]
console.log(s1.match(patt)); //null 

var s1 = 'joo';
var patt1 = /[j-mz]oo/;
console.log(patt1.exec(s1)); // ["joo"]

var s2 = 'loo';
var patt1 = /[j-mz]oo/;
console.log(s2.match(patt1)); //["loo"]

var s2 = 'noo';
var patt1 = /[j-mz]oo/;
console.log(s2.match(patt1)); //null

console.log(patt1); //[object RegExp] { ... }

console.log(patt1.toString()); //"/[j-mz]oo/"

{% endhighlight %}

You can also use test() method of regEx object to get the result true or false based on whether the match was found or not. Here is an example.

{% highlight ruby %}

var s2 = 'noo';
var patt1 = /[j-mz]oo/;
console.log(patt1.test(s2)); //false

var s2 = 'joo';
var patt1 = /[j-mz]oo/;
console.log(patt1.test(s2)); //true

{% endhighlight %}

This brings an end to the built in object topic in javascript.

References - 

https://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind#:~:text=Call%20invokes%20the%20function%20and,and%20any%20number%20of%20arguments. 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind 

https://jsbin.com/vomadedive/edit?html,js,console,output 