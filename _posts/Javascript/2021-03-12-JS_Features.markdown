---
layout: post
title:  "Basic Javascript features and its comparison with C++"
date:   2021-03-12 14:13:31 +1300
categories: Javascript
---

This article is all about javascript basics and its comparison with C++. 
Both of these languages are case sensitive and you will see many similarity and various dissimilarity between them. Obviously, we are comparing apples with oranges but they both are inherited from the fruit class. So, they cannot be poles apart. Javascript is an interpreted language whereas C++ is a compile based language. I still feel that the basics of programming cannot change drastically. Every langauage will have control blocks - if/else, for loop, etc. The internals will vary but cannot be completely altogether. The syntax will vary for sure but you will see that many syntax of C and javascript are similar. 

**Keywords**

var, true, false is a keyword in javascript. 
In C++, we don't have var keyword. We have int, float, char, bool as primitive type. However, in javascript we just have only var. The true, false are boolean type and basically we just assign this to var type. In C++, we have bool x as true, false defined in cstdbool or in C - stdbool.h. true in C is nothing but 1 and false is nothing but 0. This even holds true in javascript.

{% highlight ruby %}
var variable = 5;  //look 5 is a number in javascript or integer in C
console.log(variable);
var variable = true; //true is a boolean in javascript and in C. In C you will use bool instead of var.
console.log(variable);
{% endhighlight %}

true, false is boolean.

{% highlight ruby %}
var variable = 'text'; // text is a string in javascript. You have std::string in C++.
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

Array is a collection of values. It can be a collection of the same types or mixed types in javascript. Array is actually an object in javascript. In C++ array cannot be of mixed types. Also, the array may not be an object type in C++, if the array is a collection of int then it is not an object type. However, if the array is a collection of class type then it is an object type. Here is an example. 

{% highlight ruby %}

var var4 = [1,2,3]; // array is a collection of values.
console.log(typeof var4); // object

var var1 = [1,2,3,'4']; // collection of mixed types

{% endhighlight %}

**How to access array elements**

This is just like C or C++ language where we use subscript to access the particular element in the array. It is very similar to C except that when we access array out of boundaries in javascript then it returns undefined. In C, technically it is still undefined but in C you might get a crash or some junk value depending on how it is laid out in the memory.

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

As you can see, we got some garbage value when we accessed array out of boundaries. This is technically undefined because we can even get a crash.
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

We cannot set undefined to javascript variables. The undefined is a javascript error message. Just like in C we have array out of boundaries - bus error or in C++ we have exception thrown. When javascript cannot do something it throws undefined error.

{% highlight ruby %}
/** This is wrong **/
var var1 = undefined; // we cannot set variable to undefined.
console.log(var1); //undefined.

{% endhighlight %}

**null**

To reset a value use null. 

{% highlight ruby %}

var var1 = null;
console.log(var1); // null

{% endhighlight %}

**Is null or nullptr and undefined values are same**

Yes, the values are same but they are of different types.
In C++, nullptr is introduced in C++ 11 to avoid ambiguity. Here is an example.

{% highlight ruby %}

#include <iostream>

void func(int *a);
void func(int b);

void func(int *a)
{
   std::cout<<"func with pointer type called"<<std::endl;
}

void func(int b)
{
   std::cout<<"func with int type called"<<std::endl;
}

int main()
{
   func(NULL);
   return 0;
}

{% endhighlight %}

This doesn't compile in C++ world because we have overloaded the function func(). Now, NULL can call func(int b) as well as func(int *a) because NULL is nothing but (void *) 0. 
Look at the compilation error.

{% highlight ruby %}

$g++ -std=c++11 test2.cpp -o test2.out
test2.cpp: In function ‘int main()’:
test2.cpp:21:13: error: call of overloaded ‘func(NULL)’ is ambiguous
   21 |    func(NULL);
      |             ^
test2.cpp:7:6: note: candidate: ‘void func(int*)’
    7 | void func(int *a)
      |      ^~~~
test2.cpp:12:6: note: candidate: ‘void func(int)’
   12 | void func(int b)

{% endhighlight %}

**How do we fix the above issue?**

nullptr is a keyword introduced in C++11. This fixes the above issue described. In order to initialize pointers with some initial reset value, we use nullptr. Now, when we call func(nullptr), it will call the func(int *a). If we call func(0) then it will call func(int b). Here is the code.

{% highlight ruby %}
#include <iostream>

void func(int *a);
void func(int b);

void func(int *a)
{
   std::cout<<"func with pointer type called"<<std::endl;
}

void func(int b)
{
   std::cout<<"func with int type called"<<std::endl;
}

int main()
{
   func(0);
   func(nullptr);
   return 0;
}

{% endhighlight %}

Now, let's compile this out and run.

{% highlight ruby %}

./test2.out
func with int type called
func with pointer type called

{% endhighlight %}

In javascript, we initialize the  variable with simply null. In javascript null is nothing but an object.

{% highlight ruby %}

var x = null;
console.log(typeof x);  // object

{% endhighlight %}

**Is the value of null same as undefined**

As you can see below, the undefined type is undefined and null type is object.
However, the value is same.

{% highlight ruby %}

console.log(null == undefined); // true
var y = undefined;
console.log(typeof y); // undefined 

{% endhighlight %}

**Check the value and type together**

In order to check the value and type together in javascript, use triple equals symbol i.e. ===.

{% highlight ruby %}

console.log(null === undefined); // false

{% endhighlight %}

**NaN**

NaN means not a number. If something goes wrong with the number operation then we will get NaN. For e.g. multiplying string with number. It is more like an error message.

{% highlight ruby %}

var var1 = NaN; 
console.log(var1); //NaN
console.log(typeof var1); //  number
{% endhighlight %}

This brings end to the very basic comparison of javascript features with C++.

References - 

http://www.vishalchovatiya.com/mastering-c-books-courses-tools-tutorials-blogs-communities/ 
