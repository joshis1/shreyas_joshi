---
layout: post
title:  "Basic Javascript error handling and functions"
date:   2021-04-08 14:13:31 +1300
categories: Javascript
---

This article is all about javascript error handling and functions.

**try, catch and finally**

If you come from C++ background, then you might already be aware of exception handling. In javascript, the exeception handling is similar i.e. when you think a particular piece of code is prone to cause an exception then better put that inside the try block. For example, parsing the string as int. What if the user has passed invalid data as an input. All these code should be inside the try block. Next, catch block should catch those exceptions gracefully so that we don't kill the application unexpectedly. There is another important thing called finally, this block is useful for cleaning up the stuff. Whether there was an error or not. The final block will be exectued for sure.  Here is an example.

{% highlight ruby %}

  try{
    test(); //throws an error.
  }
  catch(e) {
    console.log('SJ - catch block ' + e.toString()); // "SJ  - catch block ReferenceError: test is not defined"
  }

  finally{
   console.log('Finally block executed'); //Finally block executed
  }

{% endhighlight %}

In order to prove the point that finally block will be executed even though there was no error, I have added one more simple example code. In this example code, the execution will never hit the catch block since there is no exception inside try block. However, the finally block will still be executed.

{% highlight ruby %}

 try{
    console.log('Hello world');
  }
  catch(e) {
    console.log('SJ - catch block ' + e.toString()); //
  }

  finally{
   console.log('Finally block executed');
  }

{% endhighlight %}

Here is the output.

{% highlight ruby %}

"Hello world"
"Finally block executed"

{% endhighlight %}

**Closures**

Closures are functions that are defined inside a function. Closures are aware of their environment. It is often used with callback because you are able to store the environment. Here is an example.

{% highlight ruby %}

function generator(input) {
   var number = input;
   return function() {
     return number*2;
   };
}

var calc = generator(900); // returns a function
var anotherCalc = generator(1000); //returns a function
console.log(calc()); //1800
console.log(anotherCalc()); //2000

{% endhighlight %}

**Immediately invoked function execution**

Also known as IIFEs, it is used to execute the function immediately.
Here is the IIFE with an example. The below code will be executed immediately and there is no need to invoke this manually.

{% highlight ruby %}

 (function calc() {
  var number = 10;
  console.log(number); //10
})();

{% endhighlight %}

**Why IIFEs are important**

IFFEs ensure that the global space is not polluted. It ensures that the variables are within the local scope only. This is pretty useful let's say we are using third party library then we would not like to have any conflict. 

**Passing value to the IIFEs**

You can pass the parameters to the IFFEs also. Here is an example. 

{% highlight ruby %}

 (function calc(input) {
  var number = input;
  console.log(number); //10
})(100);

{% endhighlight %}

**Usage of passing parameters to IIFEs**

Here is an example that illustrates the usage of passing parameters to the IIFEs. 
For example, you have a global obj. Now, you want to add the property value to the global obj. You can do this using IIFEs.

{% highlight ruby %}

var obj = {}; //declare and define an object
console.log(obj); //[object Object] { ... }

 (function calc(input) {
   input.name = 'Shreyas'
})(obj);

console.log('After IIFE is executed'); //"After IIFE is executed"
console.log(obj); // [object Object] { name: "Shreyas" }

{% endhighlight %}

**Built in methods and properties of functions**

**arguments**

arguments is a built in property of a function and it gives an object with key value pair. Key is simply index starting with 0 and the value is nothing but the argument value. So, it can be accessed like an array using index as a key. Here is an example.

{% highlight ruby %}

  function message(msg) {
    console.log(msg); //Hi
    console.log(arguments); //[object Arguments] { 0: "Hi", 1: 10}
    console.log(arguments[0]); //Hi
    console.log(arguments[1]); //10
    console.log(arguments[2]); //undefined
    console.log(arguments.length); //2
  }
  message('Hi', 10);

{% endhighlight %}

**name of the function**

You can find the name of the function using name property of the function. Also, you can use length property to find out how many arguments that function requires. This may be useful if you want to loop through an array of functions and you need to know how many arguments each function requires. Here is an example.

{% highlight ruby %}

  function message(msg) {
    console.log(msg); //Hi
  }
 
  var xFunc = message;
  console.log(xFunc.name); //"message"
  console.log(xFunc.length); //1

{% endhighlight %}

This brings an end to this topic. 

References - 

https://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind#:~:text=Call%20invokes%20the%20function%20and,and%20any%20number%20of%20arguments. 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind 

https://jsbin.com/vomadedive/edit?html,js,console,output 