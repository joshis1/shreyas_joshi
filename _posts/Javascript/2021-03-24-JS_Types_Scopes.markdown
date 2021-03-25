---
layout: post
title:  "Basic Javascript types - primitive and reference type && scope - Global and Local"
date:   2021-03-24 14:13:31 +1300
categories: Javascript
---

When you assign a value to a primitive type, then you copy a value to variable. It's just another copy and not a reference. Just like in C, C++ primitive types, a value gets copied from one variable to another variable. It's actually a separate copy. So, if you original then the another copy won't change. If you are coming from C,C++ background then you know that if you simply use pointer then the pointer will point to the same container. 
Here is the primitive type test in javascript.

{% highlight ruby %}
  
  var aNumber = 5;
  console.log(aNumber); //5

  var anotherNumber = aNumber;
  console.log(anotherNumber); // 5

  aNumber = 12;
  console.log(aNumber); //12 
  console.log(anotherNumber); //5

{% endhighlight %}

**Objects are reference type**

Objects are reference type and array is nothing but an object.
In reference type, we have a pointer that points to the memory where the data lives.
Example, if we have a variable that is assigned an object, then internally that variable doesn't hold the value but the pointer i.e an address to the memory that has a data. If you come from a C/C++ background then you can understand this. This is something happening behind the scene. An important point is that since we are storing references if you change the data then all the references pointing to that memory will be affected. So, you should keep this in mind in order to avoid any bugs. 

{% highlight ruby %}

  var array = [1,2,3];
  console.log(typeof array); //object
  var anotherArray = array;
  console.log(array); // [1,2,3]
  console.log(anotherArray); // [1,2,3]
  array.push(4);
  console.log(array); // [1,2,3,4]
  console.log(anotherArray); // [1,2,3,4]

{% endhighlight %}

**Mutable**

Mutable is a type of variable that can be changed. In javascript, only objects and arrays are mutable and not primitive types. You can make a variable name point to a new value, but the previous value is still held in memory. Hence the need for garbage collection. String and numbers are immutable in javascript. Having said that, if you re-assign an array then it is technially a new array. This array will point to new piece of memory now. Here is an example.

{% highlight ruby %}

 var array = [1,2,3];
 var anotherArray = array;

 array = ['a', 'b']; // now array points to a different piece of memory. 

 console.log(array); // ['a', 'b'] 
 console.log(anotherArray); // [1,2,3] this still points to the old piece of memory i.e. [1,2,3]

{% endhighlight %}

**Immutable**

In javascript, string and numbers are immutable. It means the values cannot be changed. It really means a value can be changed but the result will store in a new memory and the old memory will be available for garbage collection.

{% highlight ruby %}

 str = "ABC";
 str.toLowerCase();
 str_lower = str.toLowerCase(); // a new string is returned instead of changing it.
 console.log(str); // "ABC"
 console.log(str_lower); // "abc"

{% endhighlight %}

Javascript doesn't allow to change the value of a string. Here you can see that you need to assign the value to another string to see the LowerCase results.
Another example is slicing of the string. It is clear enough that string is immutable. 

{% highlight ruby %}

var str = 'string';
var newstr = str.slice(1,3); // 1 and 3 index number are not included
console.log(str); // "string"
console.log(newstr); // "tr"

{% endhighlight %}

**Scope**

This is a very important topic and the most confusing topic for a C/C++ background people. The scope of the variables in javascript. In C, C++ you three types of scope - local scope, global scope and block scope. In javascript, you just have 2 scopes i.e. local scope and global scope. This makes a life difficult for a C/C++ programmer. You can avoid this situation using let keyword. However, we will focus here without using the keyword let. 

global scope - The scope here is Window based i.e. Windows object.

local scope - This is nested within global scope.

We cannot use local variables inside a global scope.
Here is a simple example. I still want to emphasize that the scope is not blocked scope i.e not based on curly braces {}. Also, never forget the hoisting feature where you can declare a variable later but it doesn't mean that the value is initialized. If you do so then the initial value assigned will be undefined.

{% highlight ruby %}

var test = 'Global Scope';  // it's global
console.log(test); // Global Scope

function localScope() {
  var test = 'Local Scope'; // local variable because it is inside a function
  console.log(test); // Local Scope
}

localScope(); 
console.log(test); // Global Scope

{% endhighlight %}

Now, things will change if we remove var from test inside the function localScope. This happens because then we are not creating another variable but we are referring to the global variable only. Here is an example and we have removed var inside the function localScope(). 

{% highlight ruby %}

var test = 'Global Scope';  // it's global
console.log(test); // Global Scope

function localScope() {
  test = 'Still Global Scope'; // since no var it is accessing global variable test
  console.log(test); // Still Global Scope 
}

localScope(); 
console.log(test); //Still Global Scope
{% endhighlight %}

**Javascript doesn't support block scope**

Wow, this is a very big statement and coming from C background this is very confusing after floating point.
But, this is what it is and we need to understand this.
Also, keep hoisting in your mind. hoisting is declaring the variable and not defining it. So, if you use a variable before declaring and assigning it then its value will be undefined unless you assign with a value. You don't have to declare it and you can declare it later. Best to use strict mode to avoid such situations. Anyway, let's look at some interesting code.

{% highlight ruby %}

function myFunction() {
 console.log(i); // undefined 
 var i = 0; 
 console.log(i); // 0

 if(true) {
    var i = 5; // new variable now i remember primitive types are immutable that means you cannot change it. So, here you have created a new variable i.
    console.log(i); // 5
 }
 
 console.log(i); // 5 since i is not block scoped but local scoped.

}

myFunction(); //call that function

{% endhighlight %}

Here is another example that is a bit more tricky but keep in mind two things - hoisting and block scope. 

{% highlight ruby %}

  var notNull = 1; // global 
  function test() {
    if(!notNull) {
     console.log("Null-ish so far", notNull); // undefined
     for(var notNull = 10; notNull <=0 ; notNull++) { //see this var notNull=10, it is initialized here and due to hoisting it will be declared inside the function but assigned to undefined. We know that undefined is kind of flase. This is a local variable since it is inside a function.
       //.. won't ever come here.
     }
     console.log("Not it is not null", notNull); // 10 was assigned in the for loop but for loop never executed

    }
    console.log(notNull); // 10  because it is inside the function test and therefore local variable.
  }

  test();

{% endhighlight %}

Now, let's remove the var from the for loop noNull and you will see how it behaves now.

{% highlight ruby %}

 var notNull = 1; // global 
  function test() {
    if(!notNull) {  // this conditionw will be false because notNull here is a global variable.
     console.log("Null-ish so far", notNull); 
     for(notNull = 10; notNull <=0 ; notNull++) {  again we are accessing global variable notNull here because we are not declaring anything.
     }
     console.log("Not it is not null", notNull); // 1 -- since it is a global variable.

    }
    console.log(notNull); // 1 
  }

  test();

{% endhighlight %}

This brings end to the scope topic in javascript. Again, this is a confusing topic and you should spent some time if you are coming from C, C++ background.

References - 

http://www.vishalchovatiya.com/mastering-c-books-courses-tools-tutorials-blogs-communities/ 
