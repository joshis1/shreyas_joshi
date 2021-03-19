---
layout: post
title:  "Basic Javascript conditional structs and comparison with C/C++"
date:   2021-03-18 14:13:31 +1300
categories: Javascript
---

This article is all about basic javascript conditional structs. Before we dive into conditional structs let's talk about some basic features of javascript in continuation of JS features.

**object**

{% highlight ruby %}

var myobj = {
  //fields and methods
  //fields are properties
  // methods are functions
  name: 'Max'
};

console.log(myobj);

[object Object] {
  name: "Max"
}

console.log(myobj.name);

// "Max"

console.log(typeof myobj); // "object"

{% endhighlight %}

In C++, we need to declare a class first and then we instantiate it to create an object.

{% highlight ruby %}
#include <iostream>

class objTest
{
 public:
  std::string name;
};

int main()
{
  objTest myobj;
  myobj.name = "Max";
  std::cout<<"myobj.name "<<myobj.name<<std::endl;
  return 0;
}
{% endhighlight %}

***Using strict mode in Javascript**

Javascript doesn't need semicolon to terminate the statement. It can still work without even semicolon. It can use line break to figure out the end of the statement. However, it is not a good practice to omit the semicolon. We should always terminate the statement using semicolon. In C++, we will get compile time error if we omit semicolon. Semicolon helps to identify the end of the instruction. Even you can omit the keyword var when assigning the value to the variable. However, it is not a good practice. You can restrict the user not to do that by using the "use strict".

{% highlight ruby %}
  "use strict"; // forces users not to omit the semicolon and not to omit the var keyword.

{% endhighlight %}

**Other bad things allowed by Javascript**

You can change the value of the var from number to string or some other data type. This is true because javascript is loosely typed language. Unlike C++, where we cannot put string into a float variable type. In Javascript, we can do so. Here is an example. 

{% highlight ruby %}
  var var1 = 5;
  console.log(typeof var1); //number

  var1 = '10';
  console.log(typeof var1); // string

{% endhighlight %}

It is not a good practice to change the type of a variable since it makes debugging very difficult.


**Hoisting in Javascript**

It is a behaviour of moving declarations to the top. A variable can be declared after it has been used.

{% highlight ruby %}

   x = 'hello'; // Assign hello to x
   var x; //Declare

{% endhighlight %}

In C++, you cannot do that. You will get compilation error. Ideally, even in javasript you shouldn't use a variable before declaring it.

**functions in javascript**

In javascript, you can create functions using keyword function. In C++, you don't have to write this keyword function.

{% highlight ruby %}

function calc() {
 console.log('Inside calc()');
}

calc(); // caller

{% endhighlight %}

In C++, you don't say function but simply the function has a signature.

{% highlight ruby %}

 void calc() {
   std::cout<<"Inside calc()"<<std::endl;
 }

 calc();

{% endhighlight %}

function is a type in javascript. Here is the code that will show that there is a type called function.

{% highlight ruby %}

var calc = function() {
  console.log('calc');
};

console.log(typeof calc); //"function"

var anotherFunc = calc;

anotherFunc(); // calc

{% endhighlight %}

**functions with parameters**

{% highlight ruby %}

 function calc(number1, number2) {
   return number1 + number2;
 }

 var returned = calc();
 console.log(returned); //NaN

 var returned = calc(10,8);
 console.log(returned); // 18

 var returned = calc(10,8,10); // the extra parameter will be ignored

 console.log(returned); //18

 var calculator = calc;
 console.log(calculator(15,2)); //17

{% endhighlight %}

You can see that functions in javascript are more or less like C only. It is just that function is a type in javascript whereas in C there is no such keyword function. We just need signature in C or C++. In Javascript, we need function keyword.

**Control Structures**

This is all about when to execute a certain code. Basically, if, else, elseif are the control blocks. You will be surprised here that the syntax of C,C++ and javascripts are same. In fact javascript supports ternary operator too.

{% highlight ruby %}

var condition = true;
var anotherCondition = true;

 if(condition) {
   console.log('Executed');
 }
 else if(anotherCondition)
 {
    console.log('another condition executed');
 }
 else {
   console.log('nothing executed');
 }

{% endhighlight %}

Output is 

{% highlight ruby %}

"Executed"

{% endhighlight %}

Now, let's see the same thing in C.

{% highlight ruby %}

#include <stdio.h>
#include <stdbool.h>

int main()
{
        bool condition = true;
        bool anotherCondition = true;

        if(condition) {
                printf("Executed");
        }
        else if(anotherCondition)
        {
                printf("another condition executed");
        }
        else {
                printf("nothing executed");
        }
        return 0;
}


{% endhighlight %}

The output is same - 

{% highlight ruby %}

"Executed"

{% endhighlight %}

In javascript, any non-zero condition is interpreted as true and 0 is interpreted as false. This is exactly what C language interprets too. Here is an example.

{% highlight ruby %}

var condition = 234;
if(condition) {
console.log('Executed non-zero condition');
}
condition = 0;
if(condition) {
console.log('You wont see me');
}
condition = -1;
if(condition) {
console.log('Non-Zero is true condition');
}
{% endhighlight %}

Here is the output 

{% highlight ruby %}

"Executed non-zero condition"
"Non-Zero is true condition"

{% endhighlight %}

Let's do the same thing in C and see how it behaves. You will notice that the behaviour is same. Here is the code.

{% highlight ruby %}

#include <stdio.h>

int main()
{
    int condition = 234;
    if(condition)
      {
        printf("Executed non-zero condition \r\n");
      }
    condition = 0;
    if(condition)
      {
        printf("You wont see me \r\n");
      }
    condition = -1;
    if(condition)
      {
        printf("Non-Zero is true condition \r\n");
      }
    return 0;
}

{% endhighlight %}


Here is the output 

{% highlight ruby %}

 ./test_cond1.out
Executed non-zero condition
Non-Zero is true condition

{% endhighlight %}

Please note that non-zero is treated as true only in conditional statement. It doesn't mean boolean true is a non-zero value. In fact, in javascript and C language true is nothing but 1 and false is nothing but 0. But, also note that they are two different data types. The following code will explain it. Here is the javascript check.

{% highlight ruby %}
console.log(1 == true); // true
console.log(1 === true);  // false since they are different data types.
console.log(0 == false);  // true
console.log(0 === false); //false since they are different data types.

{% endhighlight %}

This brings end to the conditional struct of javascript.

References - 

Practice javascript using - 

https://jsbin.com/ 
