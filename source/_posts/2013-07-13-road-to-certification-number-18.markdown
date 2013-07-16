---
layout: post
title: "Road to Certification #18"
date: 2013-07-14 11:22
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6, Inner Classes]
---
##Inner Classes
A **regular inner class** is able to reach members of the outer class. A regular inner class is not declared static, it's not a local method inner class and it's not anonymous.
``` java REGULAR INNER CLASS
class MyOuter {
	class MyInner {}
}
```
<!-- more -->
A regular inner class can't have static fields and methods. The only way to access a inner classes is using an instance of the outer class (this of course applies event for the `main` method). Inner classes can access members of the outer class (even private).

Inside an outer class an inner class can be instantiated directly `MyInner myInner = new MyInner()`. It's not possible to do that in a static method. You need an instance of the outer class to do that.

To instantiate it outside the outer you can do `MyOuter.MyInner in = new MyOuter().new MyInner();`. When you see something like this remember to check that the access modifier of the inner class is **private**. If that is the case, you'll get a compiler error if you are in the `main` method of a different class from the outer.

For static inner class you can declare them like this: `MyOuter.MyInner myInner = new MyOuter.MyInner();`.

Inside an inner class **this** references to the inner class itself. You have to use `MyOuter.this` to access the reference of the outer instance.

Modifier you can apply to inner classes are: every modifier you can apply to a class attribute, so **final**, **abstract**, **public**, **private**, **protected**, **static** and **strictfp**.

You can declare inner classes inside an **interface**, they'll be **public static** by default and cannot use methods declared in the interface.

###Method-local inner classes
It's possible to declare inner classes inside methods ma you can use them only after you declared them (obvious but there questions about it, so better to stress it).

They can be instantiated only inside the method where it's defined. Even this type of inner classes can access members of the outer class but can use local variable only if declared **final** and initialized before using them. In this case acceptable modifiers for the class are **final** and **abstract**. 

If the method where you declared it is static, then the inner class can only access static members.

##Anonymous classes
It's possible to declare anonymous classes or interfaces. You can basically do an override of methods. You can only use in the code public members already declare in the anonymous class but you can declare new methods if you want. It's possible to implement only just **one interface**.

``` java REGULAR INNER CLASS
class MyClass {
	public void method() {}
}

MyClass a = new MyClass() {
	public void method() { super.method(); }
};
```
