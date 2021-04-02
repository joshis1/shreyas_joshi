---
layout: post
title:  "Basic Javascript Objects"
date:   2021-04-01 14:13:31 +1300
categories: Javascript
---

This article is all about javascript objects. As discussed eariler, javascript objects are nothing but reference.  

**Creation of object**

There are various ways to create an object. We will discuss all these methods to create an object here. 

**Simply notational way to create an object**

A simple way to create an object in javascript is shown below. An object consists of properties and function. Also, within an object you can have another object. Let's have a look here.

{% highlight ruby %}
  
  var person = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };

console.log(person.name); // "Shreyas"
console.log(person.details.hobbies); //["sports", "guitar", "photography"]
person.greet(); //"Hello Shreyas"

{% endhighlight %}

Here person stores the reference to the piece of memory that points to the data shown above.
Now, let's make identical memory. However, since these are two different memory their references will differ too.
Check this out.

{% highlight ruby %}
  
  var person = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };

  var person_1 = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };

  console.log(person == person1); //false

{% endhighlight %}

**How to access field value in object**

There are two ways to access the value of the property in javascript. One way is that if you know the field name you can simply use dot operator to read the property value. There is another way i.e. treating like an array. You can simply read the value using [] with the field name inside. 
They are often called associative array since each property is associated with a string value that can be used to access it. Here is an example to illustrate this.

{% highlight ruby %}

var person = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };

  var field = 'age';
  console.log(person[field]); //38
  console.log(person['details']['hobbies']); // ["sports", "guitar", "photography"]

  console.log(typeof person); //object
  console.log(typeof person.name); //string
  console.log(person instanceof Object); //true

{% endhighlight %}

Another definition of object is that it is nothing but key,value pairs including functions.

**Using new to create an object**

Another way to create an object is by using new Object(); The good part is that we can pass the prototype i.e. a parent object which we want to create an object like. Let's say we want to create another object called anotherPerson. We can create that object by passing the parent object - person. Here is an example.

{% highlight ruby %}

  var person = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };

  var anotherPerson = new Object(person);
  anotherPerson.name = 'Neha';
  anotherPerson.age = 34;
  anotherPerson.greet(); //"Hello Neha"
  console.log(anotherPerson instanceof Object); //true

{% endhighlight %}

Let's say you don't want to inherit using prototype person. You can simply pass null to the object. Here is an example.

{% highlight ruby %}

 var personUnique = new Object(null);
 console.log(personUnique); //[object Object] { ... }
 console.log(personUnique instanceof Object); // true

{% endhighlight %}

**Using Object.create to create a new Object**

Another way to create an object is using Object.create() method. 
create() is a static method. Before we dive into more I would like to let you know that prototype is a javascript form of inheritance. 
Object.prototype is a root prototype of all objects. In simpler world, it is the super class. Let's see in action.

{% highlight ruby %}

 var person = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };
 var objPerson = Object.create(person);
 objPerson.name = 'Neha';
 console.log(objPerson.age); //38
 console.log(objPerson.name); //Neha
 objPerson.greet(); // "Hello Neha"
 console.log(objPerson instanceOf Object); // true 
 console.log(Object.getPrototypeOf(objPerson)); //this object of person

{% endhighlight %}

The Object.create() way has an advantage that we can use prototype i.e. inheritance easily. You can also create an object without using prototype field i.e. by passing null. Here is an example.

{% highlight ruby %}

 var objPerson = Object.create(null);
 console.log(objPerson);
 console.log(objPerson instanceof Object); //false

{% endhighlight %}

**Prototypes**

Prototype in javascript is nothing but inheritance. Prototype has some builtin method that is available to all objects such toString(). Let's take an example.

{% highlight ruby %}

var person = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };

 console.log(person.__proto__); // [object Object] { ... }
 console.log(person.checkout); // undefined
 console.log(person.toString()); // "[object Object]"

{% endhighlight %}

The super class is actually an Object class. You can specify the prototype there so that it is available to all the objects. Prototype uses chain of inheritance i.e. prototype of prototype and so on. Here is an example.
In this example, person has a method greet() and we have also defined greet() in the super class i.e. Object. Now, when we call greet() from person object then greet() of person object is invoked. However, when we invoke greet() of an obj which is just a different object then greet() of Object.prototype is invoked. 

{% highlight ruby %}

var person = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };

 Object.prototype.greet = function() {
   console.log('Hello general ' + this.name);
 };

 person.greet(); // "Hello Shreyas" calls greet of person
 var obj = {name: 'SJ'};
 obj.greet(); // "Hello general Shreyas calls greet of Object

{% endhighlight %}

prototypes are nothing but blue prints and you can create more objects using that blue print. Here is an example.

{% highlight ruby %}

var person = {
    name: 'Shreyas', //field name and value
    age: 38,
    details: {
     hobbies: ['sports', 'guitar', 'photography'],
     location: 'Australia',
    },
    greet: function() {
     console.log('Hello ' + this.name);
    },
  };

var sj = Object.create(person);
sj.name = 'SJ';

var neha = Object.create(person);
neha.name = 'Neha';

sj.greet();   //"Hello SJ"
neha.greet(); // "Hello Neha"

console.log(sj.__proto__ == person); // true
console.log(neha.__proto__ == person); // true

console.log(Object.getPrototypeOf(sj) == person); //true
console.log(Object.getPrototypeOf(neha) == person); //true

{% endhighlight %}

**Constructor functions**

Another way to create an object is using constructor functions. This is a more preferred way than anything else. Here is the constructor function.


{% highlight ruby %}

 function Person(name, age) {
   this.name = name
   this.age = age
   this.greet = function() {
     console.log('Hello ' + this.name);
   }
 }

 var person1 = new Person('Neha',34);
 var person2 = new Person('Shreyas', 38);

 person1.greet();  // Hello Neha
 person2.greet();  // Hello Shreyas 

 Person.prototype.name = 'noname';
 console.log(person1.name); // "Neha"
 console.log(person1 instanceof Person);  //true

 Person.prototype.greetGeneral = function() {
    console.log('General Hello ' + this.name);
 };

 person1.greetGeneral(); //General Hello Neha
 person2.greetGeneral(); //General Hello Shreyas

 var person3 = new Person();
 console.log(person3.name); //undefined

{% endhighlight %}

**bind**

bind() method creates a new function that, when called has its this keyword set to provided value.
I have taken the above definition from MDN. Let's try to understand this. By default, the this points to the global window object. You can see that by printing out the this in the global scope. Similarly, try logging this within the object. You will see that this points to the reference we are taking about. Sometimes, we want to explicitly tell what this we are talking about. We can do this using bind() function. Here is an example.

{% highlight ruby %}

 function fn() {
    console.log(this);
  }

  var obj = {
   objFn: fn
  };

  var person = {
    name: 'Shreyas',
    age: 38
  };

 console.log(this); // window object
 obj.objFn(); //  obj object
 // Let's say you want to use Windows Object rather than obj object 
 obj.objFn.bind(this)(); // Now again you get Windows Object
 // Let's bind person's obj here. 
 obj.objFn.bind(person)(); // person's object you are binding now.

{% endhighlight %}

Passing multiple arguments to the function using bind() call. You can pass multiple arguments to the function if the function requires that with bind(). Here is an example.

{% highlight ruby %}

 function fn(message) {
    console.log(message + this);
  }

  var obj = {
   objFn: fn
  };

  var person = {
    name: 'Shreyas',
    age: 38
  };

 obj.objFn.bind(person, 'Hi')(); // person's object you are binding now.

{% endhighlight %}

**call() just like bind**

Well, there is a big difference between call() and bind(). When we use call(), it invokes the function and allows you to pass in arguments one by one. Bind returns a new function, allowing you to pass in a this array and any number of arguments. Here is an example.

{% highlight ruby %}

 var person1 = {
   firstname: 'Shreyas',
   lastname: 'Joshi'
 };

 var person2 = {
  firstname: 'Neha',
  lastname: 'Gaud'
 };

 function say(greeting) {
   console.log(greeting + ' ' + this.firstname + ' ' + this.lastname);
 }

 say.call(person1, 'Hello'); 
 say.call(person2, 'Hello');

 var sayHelloSJ = say.bind(person1); // "Hello Shreyas Joshi"
 var sayHelloNeha = say.bind(person2); //"Hello Neha Gaud"

sayHelloSJ('hello'); // "hello Shreyas Joshi"
sayHelloNeha('hello'); // "hello Neha Gaud"

{% endhighlight %}

**apply() is like call()**

Apply is exactly like call except that you can pass in arguments as an array whereas in call you pass in arguments one by one. They both invoke the function immediately unlike bind. Thus, bind can be used for events like based on the event we can invoke the function later. Here is an example of apply().

{% highlight ruby %}

 var person1 = {
   firstname: 'Shreyas',
   lastname: 'Joshi'
 };

 var person2 = {
  firstname: 'Neha',
  lastname: 'Gaud'
 };

 function say(greeting) {
   console.log(greeting + ' ' + this.firstname + ' ' + this.lastname);
 }

 say.apply(person1, ['Hello']); //"Hello Shreyas Joshi"
 say.apply(person2, ['Hello']); //"Hello Neha Gaud"

{% endhighlight %}

**Object.defineProperty**

According to MDN, this static method Object.defineProperty() defines a new property directly on an object, or modifies an existing property on an object, and returns the object.


With this property, you can also create a getter and setter for the property. Here is an example.

{% highlight ruby %}

 var person = {
   firstname: 'Shreyas',
   lastname: 'Joshi'
 };

 Object.defineProperty(person, "fullName", {
  get: function() {
   var fName =  this.firstname + ' ' + this.lastname;
   return fName;
  },

  set : function(fName) {
   //console.log(fName);
   var stringArray = fName.split(/(\s+)/);
   //console.log(stringArray);
   this.firstname = stringArray[0];
   this.lastname = stringArray[2];
   
  }
 });

 console.log(person.fullName); //"Shreyas Joshi"
 person.fullName = "Neha Gaud";
 console.log(person.fullName); // "Neha Gaud"
 
{% endhighlight %}

Also, you can add a property to an object using Object.defineProperty() static method. Here is an example. Let's say the account object has just withdraw function and now you want to add deposit function at the same time. This can be achieved using Object.defineProperty method. Here is an example.

{% highlight ruby %}

 var account = {
   cash: 12000,
   withdraw: function(amount) {
     this.cash -= amount;
     console.log('Withdraw ' + amount + ', new cash reserve is: ' + this.cash);
   }
 };

 account.withdraw(1000); //"Withdraw 1000, new cash reserve is: 11000"

//built in keys available for defineProperty like value.

 Object.defineProperty(account, 'deposit', {
   value: function(amount) {
     this.cash +=amount;
   }
 });

 account.deposit(3000);
 account.withdraw(0); //"Withdraw 0, new cash reserve is: 14000"

{% endhighlight %}

Other built in keys in Object.defineProperty like writable, enumerable, etc. Note by default writable is false. It means that we cannot change the property value unless we set the writable to true. Here is an example with writable set to true.

{% highlight ruby %}

 var account = {
   cash: 12000,
   withdraw: function(amount) {
     this.cash -= amount;
     console.log('Withdraw ' + amount + ', new cash reserve is: ' + this.cash);
   }
 };

Object.defineProperty(account, 'name', {
  value: '1000-1',
  writable: true  // by default writable is false.
});

console.log(account.name); //1000-1
account.name = '1000-3'; //this won't change if writable is not set to true
console.log(account.name); //1000-3

{% endhighlight %}

**Delete a property of an object**

In javascript, if you want to delete a property of an object then you can use delete keyword. Here is an example.

{% highlight ruby %}

var person = {
   name: 'SJ',
   age: 38,
   city: 'Brisbane',
   greet: function() {
     console.log('Hello ' + this.name);
   }
};

console.log(person.name); //SJ
console.log(person.age); //38
delete person.age;
console.log(person.age); //undefined
person.greet(); // "Hello SJ"
delete person.name;
person.greet(); // "Hello undefined"

{% endhighlight %}

**Determine if a particular field exists or not**

You can determine if a particular field exists in an object or not using 'in' keyword. Here is an example. 

{% highlight ruby %}

var person = {
   name: 'SJ',
   age: 38,
   city: 'Brisbane',
   greet: function() {
     console.log('Hello ' + this.name);
   }
};

console.log('name' in person); //true
console.log('NAME' in person); //false
console.log('greet' in person); //true
console.log('city' in person); //true

{% endhighlight %}


**Loop through all the properties**

Another important task in the object would be to loop through all the fields in the object. We can achieve this using in operator. Here is an example.

{% highlight ruby %}

var person = {
   name: 'SJ',
   age: 38,
   city: 'Brisbane',
   greet: function() {
     console.log('Hello ' + this.name);
   }
};

for ( var field in person){
  console.log(field + ' is ' + person[field]);
}

{% endhighlight %}

This brings an end to the elementary introduction of an object in javascript. 

References - 

https://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind#:~:text=Call%20invokes%20the%20function%20and,and%20any%20number%20of%20arguments. 

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind 

https://jsbin.com/vomadedive/edit?html,js,console,output 