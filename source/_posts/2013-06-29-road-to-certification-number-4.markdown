---
layout: post
title: "Road to Certification #4"
date: 2013-06-29 09:21
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6, Override]
---
####Still About Override
The keyword **implements** is used by a class to implement an *interface*:

* you need to follow the same rules of a [legal override](http://invasionofsmallcubes.github.io/blog/2013/06/28/road-to-certification-number-3/);
* if a class is not abstract, it has to implement every method;
* no checked exception besides the one declared on the interface (subclass exception at most)
* same signature of the interface (the return type can be a subclass of the one in the interface method), also you don't need to redeclare the checked exceptions if you're not doing something that throws it.
> ####Be aware that:
> Remember the interface example with two interfaces having the same method signature? Is this compiling?
``` java INTERFACE WITH CHECKED EXCEPTION 
interface Bounceable {
	void something() throws IOException;
}
interface Breakable {
	void something();
}
interface Someable extends Bounceable, Breakable {}
class Lol implements Bounceable, Breakable {
	@Override
	public void something(){
	}	
}
```
<!-- more -->
**A class can "extends" just one class but can "implements" one or more interfaces. An interface can "extends" one or more interfaces.**
###Legal Return Type
As we already said, when you are overloading you can change the return type as long as you're still changing the list of paramters. In an override you have to return the same type or a subclass.

You can return this values:

* it's possibile to return **null** if the return type is a class;
* it's possible to return an array;
* if the return type is a primitive it's possible to return a value implicitly convertible to that primitive. Like *int* and *char*.
* if the return type is a primitive it's possible to return anything explicitly convertible to that primitive. Like *int* and *(int) float*.

##Constructors
They do not have a return type. They have the same name of the class. If a constructor with parameters is declared, the default no-args constructor is not implicit anymore.

Let's say we have this hierarchy: Dog -> Animal -> Object (because in Java every class IS-A Object). When I call the Dog constructor here's what's happening:

* Dog constructor is called;
* Animal constructor is called (`super()`) if not declared explictly another one (like a super with parameters);
* Object constructor is called if not declared explictly another one (like a super with parameters);
* The instances of Object variables are initialized;
* Object constructor completes;
* The instances of Animal variables are initialized;
* Animal constructor completes;
* The instances of Dog variables are initialized;
* Dog constructor completes;

Rules for a constructor are:

* if the default constructor is private, a subclass cannot call `super()`, you get a compilation error;
* it's possibile to call inside a constructor (as first ) `this()` or `super()` (or one of their overloads). The compilator calls `super()` by default;
* constructors are **not** inherited;
* `super()` is always called first, you cannot even put a try catch;
