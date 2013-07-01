---
layout: post
title: "Road to Certification #5"
date: 2013-07-01 21:15
comments: true
categories: [Sun, Certification, SCJP, OSCJP]
---
##Literals
A **literal** primitive is a representation i the source code of primitive data.
###Integer Literals
They can be expressed in base 10, 8 (octal) or 16 (hex):

* decimals can be written using the range `[0-9]`
* hexadecimals can be written with the range `[0-7a-f]` with prefix `0x` or `0X` (case insensitive). Max 16 digits excluding the prefix;
* octals can be written using the range  `[0-7]` with a `0` in front of the numbers. Max 21 digits excluding the prefix;

They can have `L` or `l` after the number to indicate the type **long**.

``` java EXAMPLE OF INTEGER LITERALS
// The number 26, in decimal
int decVal = 26;
//  The number 26, in hexadecimal
int hexVal = 0x1a;
// The number -8, in octal
int octalVal = 037777777770;
```
<!-- more -->
###Floating-Point literal
Defined by default as **double** (64bit). If you want to use them as **float** you need to put `F` or `f` after the number. Their structure is `integer<dot>fraction` like `0.0f`. Declaring a float without the final *f* you get a *compiler error*.

Doubles can have at the end `D` or `d` but it is optional.

###Boolean literals
**true** or **false**. YOU CANNOT USE INTEGERS, again: YOU CANNOT USE INTEGERS, you get a compilation error.

###Character literals
Single characters between `'`. It's possible even to use Unicode characters like `char a = 'n';` is equal to `char a = '\004E';`. They are 16bit integers so it's possible to assign a char variable to an integer (range `0-65535` but remember that if you go out of range you need to cast them like this: `char a = (char)70000;` and you can do also `int a = (char)70000;`. It's possible to escape special characters like `char a = '\'';`.

> ####Be aware that:
> So 70000 in binary is equal to 0b10001000101110000, when you do something like `int a = (char)70000;` 70000 is out of range so when you cast to **char** the jvm flips the left-most digit so 0b**1**0001000101110000 becomes 0b**0**0001000101110000 which is in range and equal to 4464.

###Assignment operators
A variable can contain a primitive type or a reference to an object. In both cases it contains bits, in the first case is a value, in the second case it's a reference to the object in the heap.

It's possible to assign to a primitive variable a literal or the result of an expression. For integers if do an operation (**+ - * /**) between integers and a subtype (like byte) the expression returns always an integer.

###Primitive casting
Casts can be implicit or explicit. A cast is implicit if you are doing a widening operation (e.g.: you put a byte into an int). Explicit cast is needed when narrowing (e.g: you put an int into a byte - duh!). Doing an explicit cast is risky because you can assign out of range values. Be aware that you don't get a runtime exception, you just get the left-most bit flipped.

If you assign to a primitive a value that is too large without an explicit casting you get a compilation error.

With a **compound operator** (+=, -=, *= and /=) the cast is implicit: `b+=7` is `b=(byte)b+7` so you don't get a compilation error when doing `bit+=128;`.

If you assign a variable to another variable you are just copying the value of that variable. The two variables are not connected at all. In case of reference variable you are copying the reference of the variable and they are also disconnected:
``` java VARIABLE ASSIGNMENT
		CoffeeSize a = CoffeeSize.HUGE;
		CoffeeSize b = CoffeeSize.BIG;
		System.out.println(a);
		System.out.println(b);
		b = a;
		a = CoffeeSize.SMALL;
		System.out.println(a);
		System.out.println(b);
		
		int x = 10;
		int y = 5;
		System.out.println(x);
		System.out.println(y);
		y = x;
		x = 15;
		System.out.println(x);
		System.out.println(y);
```
