---
layout: post
title: "Road to Certification #7"
date: 2013-07-03 11:42
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##How to assign elements to an array
For arrays of primitive types, it's possible to assign those elements that you can implicitly cast to the type of the array. Here's an example:
``` java ARRAY ASSIGNMENT EXAMPLE
byte b = 4;
char c = 'c';
int[] a = new int[2];
a[0] = b;
a[1] = c;
```
In an object array is possible to assign to it everything that passes an IS-A test. So if I have `Honda extends Car` that means I can assign to a `Car[]` a `Honda` reference. Not true the other way around (not every `Car` IS-A `Honda`).

I cannot assign entire arrays if they are of different type like `int[]!=char[]`.

Multidimensional arrays can be assign to each others if they have the same declaration dimension (`int[][] a` can be assigned to `int[][] b`). Basically this compiles and runs:
``` java ARRAY ASSIGNMENT EXAMPLE
int[][]	d = new int [2][];
int[][] e = new int [3][];			
d = e;
```
<!-- more -->
##Initialization Blocks
You can have static or instance initialization blocks. They do not accept arguments and you can declare them with the following statements: `static {}` and `{}`. You can have more than one inside a class and they are executed in the order of declaration.

The static ones are called when the class is loaded, the instance ones are called after the call to `super()` in the constructor you are using.
## Wrappers

They are there to use primitive in a context where is necessary an object (like when you declare a `List`) and they also have utility methods for primitives. They are immutable (like `String`s).

Every wrappers has two constructors, one that accepts a primitive and one that accepts a `String`. Numerals wrappers accept a string number, `Boolean` accepts only "true" for **true**, the rest is evaluated to **false**. The wrapper `Characters` for *obvious* reasons does not have a `String` constructor.

The `String` constructor of numerals wrappers throws a `NumberFormatException` if the parsing fails.

###Some Useful Methods

* `static <WrapperType> valueOf(String valueOf)`: you can use it to create a wrapper from a String. Numerals have a second argument indicating the numeric base like `Integer.valueOf("110",2)`;
* `<primitiveType> primitiveTypeValue()`: like `intValue` returns the primitive value of the wrapper instance; 
* `static <primitiveType> parsePrimitive()`: like `parseInt`. It works like `valueOf()` but returns a primitive;
* `toString()`: we have the classic instance method, then we have two more: one static accepting a primitive and returning a String, the other one is just for `Integer` and `Long` that takes the primitive and the numeric base in which the string must be converted (`Integer.toString(2, 2)` returns `"10"` for example);
* `static to(Binary|Hexadecimal|Octal)String()`: for `Integer` and `Long` it prints the number in the requested base; 
