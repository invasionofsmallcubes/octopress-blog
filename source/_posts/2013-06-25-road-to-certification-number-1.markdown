---
layout: post
title: "Road to Certification #1"
date: 2013-06-26
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6, Identifiers, Code Conventions, JavaBeans, Modifiers] 
---
##Classes, methods and attributes

###Identifiers
You cannot use language keywords as identifiers. You'll have a compiler-time error.

An identifier is legal when the compiler does not complain about it. So this means that respecting the Java naming
convention is **optional**.

> ####Be aware that:
> you need to be careful when you read the question because if it does not ask specifically about naming conventions, just focus about what is legal.

An identifier is composed by *Java Letters* and *Java Digits* and it must start with a Java Letter. It is **case-sensitive**. A Java Letter is in the range `[A-Za-z_$]` and a Java Digit is in the range `[0-9]`.

> ####Be aware that:
> The [Java Language Specification](http://docs.oracle.com/javase/specs/jls/se7/html/jls-3.html#jls-3.8) states that: *Letters and digits may be drawn from the entire Unicode character set, which supports most writing scripts in use in the world today, including the large sets for Chinese, Japanese, and Korean. This allows programmers to use identifiers in their programs that are written in their native languages.*

<!-- more -->
###Java Code Conventions
You really need to understand what [CamelCase](http://en.wikipedia.org/wiki/CamelCase) is to get this paragraph :)

* *Classes* always start with a capital letter and if you have a class composed by two or more words they follow the CamelCase rules, like `MyCoolClass`. 
* *Interfaces* are like classes but you need to use an adjective like `Comparable`. 
* *Methods* use camelCase and use the couple verb-noun, like `getSomething()`. 
* *Constants* (variables marked `static` and `final`) use capital letters and the _ is used to separate words, like `MAX_SIZE`.

###JavaBeans Standards
JavaBeans are classes with properties. You can read and write these properties using the so-called *getters* and *setters* methods.

A getter follows the get*Property* naming convention and the signature is `public <PropertyReturnType> getProperty()`.

A setter follows the set*Property* naming convention and the signature is `public void setProperty( <PropertyReturnType> property)`

A listener has add and remove methods. The naming conventions are add*EventName*Listener and remove*EventName*Listener and the respective signatures are: `public void addEventNameListener(<EventNameListener> eventListener)` and `public void removeEventNameListener(<EventNameListener> eventListener)` so remember that you have to pass the listener as argument of the method in both cases. 

###Source File Composition

* in a source file only one class can be declared *public* and the class name equals to the file name
* we have a **package**, then the **import**s , then the class. *package* and *import*s are optional
* **import**s are per file, not per class
* if you don't have a public class then you can name the source file as you like

###Class Access Modifier
A class can have a *default* access or a *public* access:
* **default access**: we have a package level visibility. The class can be seen only from inside the package. 
* **public access**: we can see the class from every package. Remember though that public doesn't mean that you don't need to import the class first.

You can avoid importing a class when it is in the same package of the class where you want to use it.
Terrible phrasing, I'm sorry. Here's an example:

``` java IMPORT EXAMPLE SAME PACKAGE
package com.oscjp.defaultclassmodifier.externalaccess;
public class MyExternalClass {}

package com.oscjp.defaultclassmodifier.defaultaccess;
public class SomeOtherClass {
	/**
	 * No compiler error!
	 */
	MyDefaultClass myDefaultClass;
}
```

###Class (non-access) modifier
You can use the following modifiers in combination with access modifiers:
* **strictftp** can be used on classes, interfaces or methods. You can read more about it [here](http://en.wikipedia.org/wiki/Strictfp);
* **final** can be used on classes, methods or variables. A final class cannot be extended, a final method cannot be overridden, a final variable cannot be reassigned;
* **abstract** can be used on classes or methods. An abstract class cannot be instantiated (compilation error) and an abstract method is not implemented and *only abstract classes can have abstract methods (compilation error otherwise*
``` java IMPLEMENTED AND ABSTRACT METHOD
void someMethod() {/* implementation */}
...
abstract void someMethod(); /* notice the ";" at the end*/

```

###Declaring an interface
An interface is a contract a class must obey. The class must **implement** it. Here's the rules for an interface:
* methods defined in an interface are implicity *public* and *abstract*. You cannot use *static* on a method because a static method is not inherited so it won't make sense;
* all variables are implicity *public*,  *static* and *final* so remember that they need to be initialized, are not inherited by classes implementing that interface and cannot be reassigned;
* you cannot declare methods *final*, *strictftp* or *native*
* an interfaces can **extends** one or more interfaces
``` java EXTENDING AN INTERFACE
interface Bounceable {
	void something();
}
interface Breakable {
	void something();
}
/**
 * notice that it doesn't matter they have the same
 * method name because the class will just have one
 * implemented method
 */
interface Someable extends Bounceable, Breakable {}
```

Also notice that `public abstract interface Bounceable` equals to `public interface Bounceable`.
