---
layout: post
title:  "Object_Oriented_Design"
date:   2016-01-11 14:13:31 +1300
categories: Design_Patterns
---
This article is all about Design Principles.

Why do we need Software Design Principles?

These are the principles that should be used to avoid a bad software design.

Properties of Object Oriented language

1. Encapsulation – It refers to packing of data and functions into a single
component . This is done in the class.
2. Data Hiding – Data cannot be manipulated or read directly. It needs getter
and setter methods to read the member variables.
3. Abstraction – With the help of interfaces, it hides the inner complexity, and
only the public interfaces are available to the outside world. This is called
Abstraction.
4. Dynamic binding – With the help of V-table, a linking of function happens
at run-time. Also, it is called run-time polymorphism. Or you can say it is late
binding.
5. Inheritance – It is the feature to re-use a particular class.
6. Polymorphism – An ability of an object, function, and operator to take
many forms is called polymorphism. Early binding/compile time polymorphism.
These are classified as the following.
a)Method overloading. : A behaviour may vary based on the input data type.
b)Operator Overloading : An operation may vary based on the instance.
With the aid of polymorphism, you program in a generic way and not a specific
way. Thus, you decouple the code. For example, using interface to refer to
the specific/concrete class makes the code loosely coupled.
Drawbacks of a tightly coupled code?
a. Rigidity – Basically, it means tightly coupled. When you change one piece
of code, everything needs to be changed.
b. Fragility – Since a code is tightly coupled, one change can lead to break of
the entire system. So, code is very fragile and is succumbed to the break
down of entire system.
c. Immobility – Since it is tightly coupled, it cannot be re-used by other
application.

Object Orient ed Design Principles are called “SOLID“.

SOLID stands for –

a. S – Single Responsibility. <br>
b. O – Open Closed. <br>
c. L – LISKOV Substitution. <br>
d. I – Interface Segregation. <br>
e. D – Dependency Inversion. <br>

Single Responsibility Principle (SRP) – It states that each class should have a single responsibility, and the responsibility should be encapsulated. A
class should address/focus only one concern. For example, a class
responsibility is used to fetch the data. Other class responsibility is to process the data. The class shouldn’t club the two responsibilities into one class – fetching the data and processing of the data. With this, you decouple
the code. Also, the test cycle can be reduced depending on the changes done.
Thus, you reduce the risk of any software changes by apprehending the
possible cause.

(Polymorphism)Open/Closed Principle (OCP) – It states that classes and
methods should be allowed for extension. However, they shouldn’t be allowed
for modification.This is mainly related to inheritance – code re-usability.
Here, the abstract interface can be re-used/extend through inheritance.
However, the existing implementation is closed for modification.
At the same time, the new implementation for the interface can be done – ext ension. By religiously following this principle, we avoid the repetitive tasks like – code review and unit-test for the well proven code.

LISKOV Substitution Principle (LSP) – It states that the object should be
replaceable with its subtype without altering the base class. This principle
helps to identify whether inheritance is really applicable or not . You may
mistakenly think that the part icular object is a type of an object .
However, the litmus test for inheritance is by applying LISKOV substitution. In short , when you identify that there is a need to change the base class in order to do the inheritance, then you violate ‘LISKOV Substitution Principle.’ Here is a classic example taken from Stack overflow – In mathematics, a square is a kind of a rectangle, whose sides are equal. Since you read “is a” relationship, a
first thought comes in mind is inheritance. However, the square doesn’t need to
set height and width separately. In square, setting one side is enough. Thus,
you cannot sub-class rectangle as square. According to LSV, if a base class
cannot be replaced with a sub-class then we should not use inheritance. In
short , we should use inheritance based on behaviour(verb – action/methods )
and not based on properties(member variables/noun). In my opinion, if you
cannot reuse many existing methods of a base class, then sub-classing is
meaningless. Also, if there is any need to change a base class to
accommodate a sub-class, then question yourself – “Is inheritance really
applicable here.” Generally, the answer is no.

Interface Segregation Principle (ISP) – It states that a client should not
depend on the methods that they don’t use. Again, this is related to
inheritance, we should not have a polluted or fat interfaces, which means that
the interface shouldn’t have methods that are unrelated or not required. We
shouldn’t clutter the interface class with the methods, which are not
related to the interface/class responsibility. Otherwise the class, which will implement the interface, has to unnecessary implement the un-related methods.
The methods, which are not related should be in the other interface. Thus, it is all about interface segregation.

[Example] – Here is a short program – ” the method get DttInfo() is not related
to contentMgr”. Thus, we have a separate interface for getting DttInfo(). This
program shows that the interface is segregated. There are two separate
interfaces – IcontentMgr and IdttInfo rather than combining the functionality
into one interface. Here the interface is segregated as the methods are
unrelated. The two interface classes are IdttInfo and IcontentMgr. The IdttInfo
is all about the dtt information. The IcontentMgr is all about content . They
are both unrelated, and they should have a separate interface.

{% highlight ruby %}

#include<iostream>
class IdttInfo
{
 public:
    virtual bool isDttSupported() = 0;
};

class serviceMgrDttInfo:public IdttInfo
{
  public:
      virtual bool isDttSupported()
{
  return true;
}

};

class IcontentMgr
{
  public:
      virtual std::string getClassName() = 0;
};

class serviceContentMgr: public IcontentMgr
{
  private:
      IdttInfo * p_mDttInfo;
      serviceContentMgr();
  public:
      virtual std::string getClassName()
{
  return "serviceContentMgr";
}
serviceContentMgr(IdttInfo * pDttInfo):p_mDttInfo(pDttInfo)
{

}
};

int main()
{
  IdttInfo * pDttInfo = new serviceMgrDttInfo;
  IcontentMgr * pContentMgr = new serviceContentMgr(pDttInfo);
  std::cout<<pContentMgr->getClassName()<<std::endl;
  std::cout<<pDttInfo->isDttSupported();
  return 0;
}

{% endhighlight %}

Dependency Inversion Principle ( DIP) - This principle states that the high
level module shouldn’t depend on the low level modules directly. Instead, a
high level class should use interface class of a low level class in order to
abstract the direct call to a low level class. With the aid of this principle,
we decouple the software modules. When you decouple the modules, the
maintenance becomes easier. This principle should only be applied when you
think that the code can change in future. However, when you know that the
code may not change in future, there is no point of creating an extra class i.e.
Interface class for every class.

High Level Classes -> Abstraction via. Interface class of a Low Level Class -> Low Level Classes

This brings an end to the topic of Design Principles/Concepts in OOPs.
