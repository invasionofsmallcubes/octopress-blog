---
layout: post
title: "Road to Certification #3"
date: 2013-06-28 21:36
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Enum
You can declare an *enum* inside a class or in a dedicated file. You can't declare it inside a class method.
If you have the following code:
``` java ENUM EXAMPLE
public class MyPublicClass {
	public enum CoffeeSize {
		SMALL, BIG, HUGE
	}
}

// you can call this enum
// In an a class in a different
// package like this:
import com.oscjp.defaultclassmodifier.defaultaccess.MyPublicClass.CoffeeSize;
CoffeeSize size = MyPublicClass.CoffeeSize.BIG;
```
Every enum has the static method `values()` that return an array 
of the enum elements in order of declaration. 
<!-- more -->
You can also have methods and you can 
override them for a specific element like this:
``` java ENUM OVERRIDE EXAMPLE
public enum CoffeeSize {	
	HUGE {
		@Override
		public String getCode() {
			return "R";
		}
	}, BIG;
	
	public String getCode() {
		return "B";
	}
}
```
> ####Be aware that:
> Really weird (well not if you understand the concept of [enum](http://docs.oracle.com/javase/tutorial/java/javaOO/enum.html)) but you can do this:
	public static void main(String[] args) {
		CoffeeSize a = CoffeeSize.SMALL;
		CoffeeSize b = a.BIG;
	}


##A little bit of OOP principles
In the certification there is some question about OOP principles: *encapsulation* and *inheritance*.

With inheritance is possible to use methods from a superclass and override them when necessary. With encapsulation you basically apply the
principle to access the state of your object in a controlled way, giving to a private attribute of your class an access from the outside using specific methods called getters and setters.

###Relationships between classes
We have two kind of relationship:

* **IS-A**: it's about inheritance and interfaces (keywords are **extends** and **implements**);
* **HAS-A**: A has a reference to B, so A *HAS-A B*;

In Java a class is always polymorphic because passes the IS-A tests for `Object` and itself.

A variable cannot change its type but can point to a reference of a subtype, like `Animal a = new Dog();` (Dog is extending Animal! `a` can only use methods from the superclass `Animal` because at compile time there is not way for the compiler that that variable has been initialized with a subclass.).

With inheritance comes the concept of [polymorphism](http://en.wikipedia.org/wiki/Polymorphism_%28computer_science%29). So if Dog is calling the method `animalSound()`, if this method is overridden in Dog then `a.animalSound();` will actually call the Dog's `animalSound()`.

In Java multiple inheritance is not available.

####Override
These are the rules for a legal override:

* same list of parameters;
* same return type or a subclass (if you are using primitives if your method return a *long*, the overridden method cannot return an *int* or viceversa);
* an overridden method cannot have a stricter access then the parent method;
* the access level can be less restrictive (if the parent has a *default* access then the child can have a *public* access);
* can throw unchecked exceptions;
* checked exceptions only if they're equals or subclass of the ones thrown by the parents;
* you don't override a method if it's final or static;

####Overload
A method must change the list of the parameters. Optionally you can change the return type, the access modifier and throw new exception.

> ####Be aware that:
> In case of overridden method, which method is going to be called is decided at runtime. In case of overload method, the method is decided at compile time because the number of parameters is meaningful.

####Casting
A **downcast** is when you go down the inheritance three, like `Animal a = new Dog(); Dog b = (Dog) a;` whereas an **upcast** is when you go up in the inheritance tree so you don't have to cast explicitly.

Generally speaking upcasting is not that useful but actually it comes to hand when you need to invoke a specific method. Let's say you have something like:
``` java
public void doIt(Object o){}
public void doIt(String s){}
```
and you have a String object. Then you want to call the first of the two method you need to do this: 
``` java UPCASTING 
String s;
doIt((Object) s);
```
Another reason could be the following one, I'm not explaining it because it would be a spectacular question on the exam, so I leave it to the reader:
``` java UPCASTING
int i = 1;
int c = 2;
i+c;
// ->(int) 3
((long)i)+c
// ->(long) 3
```
