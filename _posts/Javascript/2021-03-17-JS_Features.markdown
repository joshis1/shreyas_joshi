---
layout: post
title:  "Basic Javascript features and its comparison with C++"
date:   2021-03-17 14:13:31 +1300
categories: Javascript
---

This article is all about javascript basics and its comparison with C++.
Both of these languages are case sensitive and you will see many similarity and various dissimilarity between them. Obviously, we are comparing apples with oranges but they both are inherited from the fruit class. So, they cannot be poles apart. Javascript is an interpreted language whereas C++ is a compile based language. I still feel that the basics of programming cannot change drastically. Every langauage will have control blocks - if/else, for loop, etc. The internals will vary but cannot be completely altogether. The syntax will vary for sure but you will see that many syntax of C and javascript are similar. 

**Keywords**
var, true, false is a keyword in javascript. 
In C++, we don't have var keyword. We have int, float, char as primitive type. However, in javascript we just have only var. The true, false are boolean type and basically we just assign this to var type. In C++, we also have true, false defined in cstdbool or in C - stdbool.h. true in C is nothing but 1 and flase in c is nothing but 0. This even holds true in javascript.

{% highlight ruby %}
var variable = 5;  //look 5 is a number or integer in C
console.log(variable);
var variable = true; //true is boolean in javascript and C
console.log(variable);
{% endhighlight %}

true, false is boolean.

{% highlight ruby %}
var variable = 'text'; // text is a string in javascript.
console.log(variable);
{% endhighlight %}

**typeof**
The floating point and integers are called numbers in javascript.
In C++, we have float and int keywords. However in javascript there is no distinction. It is simply numbers in javascript.

{% highlight ruby %}
var var1 = 6.5;
console.log(typeof var1); // number

var var2 = 'text';
console.log(typeof var2); // string

var var3 = true;
console.log(typeof var3); // boolean

{% endhighlight %}

**typeid**
In C++, we have typeid to check the typeof the variable.
It is used in RTTI i.e. run time type identification.

{% highlight ruby %}

#include <typeinfo>
#include <iostream>


class myclass
{
  int mynumber;
  float myfloat;
};

int main()
{
  int myint = 10;
  float myfloat = 1.2;
  char mychar = 'a';
  std::string mystring = "My String";
  int arr[3] = {1,2,3};
  myclass myclass_instance;
  std::cout<<"Type of myint is "<<typeid(myint).name()<<std::endl;
  std::cout<<"Type of myfloat is "<<typeid(myfloat).name()<<std::endl;
  std::cout<<"Type of mychar is "<<typeid(mychar).name()<<std::endl;
  std::cout<<"Type of mystring is "<<typeid(mystring).name()<<std::endl;
  std::cout<<"Type of arr is "<<typeid(arr).name()<<std::endl;
  std::cout<<"Type of myclass_instance is "<<typeid(myclass_instance).name()<<std::endl;
  return 0;
}

{% endhighlight %}

Here are the results.

{% highlight ruby %}

 ./test1.out
Type of myint is i
Type of myfloat is f
Type of mychar is c
Type of mystring is NSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEE
Type of arr is A3_i
Type of myclass_instance is 7myclass

{% endhighlight %}

**Arrays**
Array is a collection of values. It can be a collection of the same types or mixed types. Array is actually an object.
Here is an example. 

{% highlight ruby %}

var var4 = [1,2,3]; // array collection of values.
console.log(typeof var4); // object

var var1 = [1,2,3,'4'];

{% endhighlight %}

**How to access array elements**
This is just like C or C++ language where we use subscript to 
access the particular element in the array. It is very similar to C except that when we access array out of boundaries then in javascript it returns undefined. In C, technically it is still undefined but in C you might get a crash or some junk value depending on how it is laid out in the memory.

{% highlight ruby %}

var var4 = [1,2,3]; // array collection of values.
console.log(var4[0]); // first element in the array.

console.log(var4[4]); // undefined.

{% endhighlight %}

Example in C - Array out of boundaries 

{% highlight ruby %}

#include <stdio.h>

int main()
{
   int x[] = { 1,2,3};
   printf("The first value is x[0] = %d\r\n", x[0]);
   printf("Array out of bounds 4th element = %d\r\n", x[4]);
   return 0;

}

{% endhighlight %}

The result I saw was - 

{% highlight ruby %}

 ./test2.out
The first value is x[0] = 1
Array out of bounds 4th element = 545694709

{% endhighlight %}

As you can see, we got some garbage value when we accessed
array out of boundaries. This is technically undefined because we can even get a crash.
Example - 

{% highlight ruby %}
#include <stdio.h>

int main()
{
   int x[] = { 1,2,3};
   printf("The first value is x[0] = %d\r\n", x[0]);
   printf("Array out of bounds 4th element = %d\r\n", x[432423423]);
   return 0;

}

{% endhighlight %}

Now, when I run it , I get a bus error - crash since I am accessing some unreachable memory.

{% highlight ruby %}
 ./test2.out
The first value is x[0] = 1
Bus error
{% endhighlight %}

**Undefined in javascript**
We cannot set undefined in javascript.
The undefined is a javascript error message.
Just like in C we have array out of boundaries 
or in C++ we have exception thrown. 
When javascript cannot do something it throws
undefined error.

{% highlight ruby %}
/** This is wrong **/
var var1 = undefined; // we cannot set variable to undefined.
console.log(var1); //undefined.

{% endhighlight %}


