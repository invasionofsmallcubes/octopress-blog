---
layout: post
title: "Road to Certification #8"
date: 2013-07-04 12:30
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6, Autoboxing, Wrappers, Garbage Collection]
---
##Autoboxing, *==* and *equals()*
Today we will talk a bit more about wrappers. Autoboxing is the concept that allows you to do something like:
``` java AUTOBOXING
Integer x = new Integer(1000);
x++;
```
If you remember, we said that wrappers are immutable, so what we wrote should not work because the new object should not be inside `x` but should be lost because we did not assign it to a new variable. Also using the post-increment operator could not be possible unless `++` overloading it's possible.

It's actually the JVM that does all that: we have a `Integer` x. When we use the post-increment operator, the JVM unbox the value from the wrapper, applies to it the operator, creates a new `Integer` with the incremented value and than assigns it to `x`. Still doubts? Just try this then:
``` java JVM AUTOBOXING SKILLS
Integer y = new Integer(1999);
Integer x = y;
System.out.println(x == y);
y++;
System.out.println(x == y);
```
<!-- more -->
For wrappers equality is defined as having the same value and therefore the same primitive type. As we saw you really need to be careful in using the operator `==` because you can have surprises:
``` java == OPERATOR AND WRAPPERS
Integer a = new Integer(126);
Integer b = new Integer(126);
System.out.println(a == b); // false
			
a = Integer.valueOf(126);
b = Integer.valueOf(126);
System.out.println(a == b); // true
			
a = Integer.valueOf(1260);
b = Integer.valueOf(1260);
System.out.println(a == b); // false
```
> ####Be aware that:
> The [Java Language Specification](http://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.7) says: if the value p being boxed is true, false, a byte, or a char in the range \u0000 to \u007f, or an int or short number between -128 and 127 (inclusive), then let r1 > and r2 be the results of any two boxing conversions of p. It is always the case that r1 == r2.
> 
> Ideally, boxing a given primitive value p, would always yield an identical reference. In practice, this may not be feasible using existing implementation techniques. The rules above are a pragmatic compromise. The final clause above requires that certain common values always be boxed into indistinguishable objects.  
> The implementation may cache these, lazily or eagerly. For other values, this formulation disallows any assumptions about the identity of the boxed values on the programmer's part. This would allow (but not require) sharing of some or all of these references.

> This ensures that in most common cases, the behavior will be the desired one, without imposing an undue performance penalty, especially on small devices. Less memory-limited implementations might, for example, cache all char and short values, as well as int and long values in the range of -32K to +32K.

If you compare a primitive and a wrapper, the wrapper gets unboxed and compared. If you have a method with the signature `public void do(int x) {}` then if you try something like this you're getting a `NullPointerException`: `Integer x; do(x);` because you cannot unbox a **null** value.

##Overloading when you pass parameters
When you pass parameters you should think about three features of the language and how they relate to the signature of the method and to the type of the parameter actually passed as argument:

* **widening** is when you have a **short** parameter and the method has an **int** argument. You are elevating a **short** to an **int** and it's ok because it's a subset;
* **autoboxing** is in the field when we are using wrappers;
* **var-args** is when we have a variable numbers of elements of the same type;

If a match does not exist, then the JVM tries to find the closest one among the wider ones that can found. In the previous example we saw a **short** promoted to **int**. If we had just a `public void do(double x)` then **short** will be promoted to a **double**.

If have *boxing* in the way, where possible **widening has precedence over boxing**. This means that if I have method that takes an `Integer` and a method that take a `long` and we are passing an `int`the *long method* will be called.

Widening wins also with var-args and boxing wins with var-args. Var-args will be considered as a last resource to maintain retro compatibility.

If we are just considering objects then widening is in place where widening means passing the IS-A test.

If we have boxing+widening it really depends on the specific case, you really need to exercise in this case. What happens here?
``` java JVM AUTOBOXING SKILLS
public void doIt(Long a) {}
...
byte b = 0;
doIt(b);
```
We do not have a method suitable for a byte so the boxing elevates **byte** to a **Byte** but `Byte IS-A Long` is **false** so it won't compile. The real error is *The method doIt(Long) in the type MyExternalClass is not applicable for the arguments (Integer)*, after what we said, can you explain why it does say *Integer* and not *Byte*?

##Garbage Collection
Java handles automatically memory through the process of garbage collection using the JVM. Programmer is not in controll of it. The heap is the only area in the memory interested in garbage collection that wants to eliminate unused objects.

*An object is eligible for garbage collection only when no live thread can access it*, meaning there is no reference pointing at it.

You can make an object available for garbage collection in two ways:

* set to **null** every reference to that object;
* reassign all reference pointing to that object;

Objects created inside a method stops to exists when the method exits. If object *a* has an attribute referring to object *b* but *a* is not referred by any other object, then *b* is eligible for garbage collection.
