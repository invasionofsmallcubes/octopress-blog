---
layout: post
title: "Road to Certification #6"
date: 2013-07-02 19:02
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6, Arrays, Assigning]
---
##More on Variables
###Variable scope
There are four base scopes:

* **static variables** are created when the class is loaded and stay there until removed by the JVM;
* **instance variables** are alive until the instance has been removed;
* **local variables** are valid until the method is in the stack;
* **block variables** are valid until the block is in execution;

> ####Be aware that:
> You really need to be careful about **variable shadowing**: calling two variables in different scopes with the same name. The first one called is the one in the more internal scope.
<!-- more -->
###Variable initialization
Instance variables (objects or primitives) have a default value:

* Object reference has **null**;
* byte, short, int and long have **0**;
* boolean has **false**;
* char has **'\u0000'**;
* array has **null** (it's an object). The elements of an array are initialized to the default value of their type;

Local variables (of any type) do not have a default value. They must be initialized before using them. You get a compiler error otherwise. If you declare but not using them, then you have just a warning, no error. (Still, you should not declare things you are not going to use). A local variable, if initialized inside a block, counts like a non-initialized variable. 

The different behavior is due to the fact that it doesn't make sense to have a variable without a value and the compiler is helping you when gives a warning. It would be useful even in case of an object but the compiler has no way to know when an attribute is initialized.

###Assign an instance variable
References are variables that point to an object. If I assign a reference to another reference, they both point to the same object. The assigned variable contains a copy of the reference. The object remains unique.

###Arrays declaration, initialization and construction
Arrays are objects in the heap and they can contain both primitive and objects. Arrays can be multidimensional.

Here's how you can legally declare an array: `int[] key;`, `Thread threads[];`, `String[][][] oc;`, `String[] hello [];`.
You do not declare the dimension of the array during a declaration.

An array can be constructed using the keyword **new**. You always need to define the dimension of the array in this case:
`int[] key = new int[4];` or  `int[] key; key = new int[4];`.

*Remember that in case you are declaring an array of `Object`, in the heap you create only the "array object" whereas the elements are initialized to null.*

In case of a multidimensional array you always have to specify the dimension of the first array like this: `int[][] ar = new int[3][];` and then `ar[0] = new int[3]`;.

Arrays are 0-indexed. You have an *ArrayIndexOutOfBoundException* if the index doesn't exist. Arrays have an attribute called **length**. 

It's possible to declare directly elements of an array: `int[]x = {1,0,10};` or multidimensional `int[][] a = { {1,0},{1,2,3},{3,4} };`. In this case you don't need to specify the dimension (the compiler can guess it).

You can also declare anonymous arrays like this: `int[]a = new int[]\{4,7,2\};`.
