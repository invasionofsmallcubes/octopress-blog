---
layout: post
title: "Road to Certification #2"
date: 2013-06-27 21:07
comments: true
categories: [Sun, Certification, SCJP, OSCJP] 
---
##Modifiers For Class Members
###Access Modifiers
* **public**: a method or a variable can be accessed anyway;
* **private**: a method or a variable is visible only inside the class. If a class method is private, a subclass can have a method with the same signature but it's not an *override*, it's just a normal method;
> ####Be aware that:
> you should always declare your attributes private and use getters and setters. Read more about [encapsulation](http://en.wikipedia.org/wiki/Encapsulation_%28object-oriented_programming%29).
* **protected**: a method or a variable has package level visibility and subclass visibility even if they are in different packages;
* **default**: a method or a variable has package level visibility. It's not a keyword;
<!-- more -->
###Non-access Modifier For Class Members
* **final**: used on methods implies you can't override them in the subclasses. Used on variables remove the ability to reassign them to other values. Be aware that in case a variables point to an object, you just can assign to it a new object but you can modify the state of the object;
* **abstract**: used on methods implies the method is not implemented. When a method is abstract the class *must* be abstract or you'll have a compilation error;
* **static**: used on methods or variables indicates it's a class level member. Since you cannot override class level members, you cannot use static with abstract;
* **synchronized**: used on a methods, allows only one thread to access it at the time. You can use it also with code blocks.
* **strictfp**: we saw that on classes, we can also use it on methods;
* **transient**: you can use it on class attributes to specify that they must not be considered during serialization (more on this in future posts);
###Var-args
`void myMethod(int...x) {}` has as parameter a var-arg. You can pass it an arbitrary number of arguments of a specific type. If you have more parameters, var-args must be the last of them in the signature of the method. You can pass both primitives and objects. The following code is valid:
``` java VAR-ARGS
public void foo(int i, String... strings) {
	String[] someStrings = strings;
}
```
###Constructors
They do not have a return type, they can accept arguments, var-args included. They cannot be *abstract*, *final* or *static* because they must be implemented (you even have a default constructor if not explicitly declared), cannot be overridden and it's bound to a class instance.
##Primitives
We have **byte**(1 byte), **short**(2 bytes), **int**(4 bytes), **long**(8 bytes), **float**(4 bytes), **double**(8 bytes). They are **SIGNED** ,so be aware of the range of values they can accept, you can read more about it [here](http://www.cafeaulait.org/course/week2/02.html).

We also have **boolean** primitives that can accept only *true* and *false*. In Java *false* is different from *0*, you always have to check for boolean values in conditional controls (like `if..else` or `while`).

And then we have **char**, 16-bit unicode characters. They can be used as integers with values from 0 to 65535.
###Instance Variables
They can have all four access modifiers, can be *final* and *transient*. They have a default value. They cannot be *abstract*, *synchronized*, *strictfp*, *native* and *static*.
###Local Variables
They are in the stack and can be final and you must initialize them when you want to use them. If you don't do it you'll get a compile-error.
###Array declaration
They are objects and are in the heap. They can contain both objects and primitives and if you don't initialize the elements they get a default value. You can declare them like this:
``` java VALID ARRAY DECLARATIONS
int[] x;
itn x[];
int[][] x; // multidimensional array
int[] x = new int[5]; // dimension goes
//in the constructor, not in the declaration

/**
* The following is legal, array is an object
*/
public Object returnArray() { int[] x; return x; }

```
