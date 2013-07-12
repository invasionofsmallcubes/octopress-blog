---
layout: post
title: "Road to Certification #17"
date: 2013-07-13 19:41
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Generics
`List myList = new ArrayList()` can accept any type of object (never primitives - well, with wrappers). With the usage of generics you are bound to declare the type of the Elements contained at compile time so we get compilation errors if we try to add a something different from what we defined.
<!-- more -->
###Mixing Generics with non Generics
`public List insert(List a) { a.add(new String("62"); }` it's a method that would compile without error and we would not get any type of runtime exception because of the type erasure. At runtime we basically do not have any kind of protection. The compilers remove the generics declaration and automatically puts every necessary casts that a compile time we don't use because of the generics.

> ####Be aware that:
> A sample code to understand type erasure is available on [stackoverflow](http://stackoverflow.com/questions/339699/java-generics-type-erasure-when-and-what-happens). Basically let's say I have the following code`List<String> list = new ArrayList<String>(); list.add("Hi"); String x = list.get(0);`, the compiler actually transform it like this `List list = new ArrayList(); list.add("Hi"); String x = (String) list.get(0);` so basically you don't have any way to know at runtime that the object `list` contains strings. Also check this [link](http://www.angelikalanger.com/GenericsFAQ/FAQSections/TechnicalDetails.html#FAQ001) from Angelika Langer.

###Polymorphism with Generics
With a simple array is perfectly fine to do something like `Parent[] arr = new Child(3)`, but you will get beaten if you try to do `List<Parent> list = new ArrayList<Child>();`.

When you declare a method accepting as argument a `List<Parent>` I can use as a parameter only a variable declared `List<Parent>`. Obviously at runtime the list can contain `Child` elements.

If we declare `Animal[] arr = new Dog[3];` and I can pass it to a method having as argument a `Animal[]` and I can even do `arr[0] = new Cat()` and it would compile fine. I will have an `ArrayStoreException`.

If we want to pass a subtype of the argument we can use the keywords **extends** and **super** in the definition of the method. An example is `public void addAnimal(List<? extends Animal> list) {}` where I can pass without problem a `List<Dog>` but we cannot use the method `add` inside the method:
``` java IMPOSSIBLE TO USE ADD
public class Animal {
	public void addAnimal(List<? extends Animal> list){
		list.add(new Animal());
	}
}
```
with the following error:
> The method add(capture#1-of ? extends Animal) in the type List<capture#1-of ? extends Animal> is not applicable for the arguments (Animal)
It's actually quite simple to explain it. The JVM understand that you are passing some kind of list containing `Animal` or one of its children, like `Dog`. Can you add an `Animal` to a `List<Dog>`? Nope, you can't, Dog is more specific, so you should explicitly cast it. You're saying to the JVM that you can pass to the method a wide range of List and cannot assure the safety of the `List`.

With `List<? super Dog>` you can do something like that because you can pass to as argument of the method at minimum a `List<Dog>` or something higher in the hierarchy, like `List<Animal> you have guarantee that `Dog` IS-A `Animal` so it's ok.

What will happen here?
``` java SUPER EXAMPLE
public class Animal {
	public void addAnimal(List<? super SpecificDog> list){
		list.add(new SpecificDog());
		list.add(new Dog()); // same error as above!!
		// the JVM cannot know if the list can accept Dogs
		// because you have a probability there
		// to have a List<SpecificDog>
		// YOU CAN ADD A SPECIFICDOG or its subtypes!
	}
}
class Dog extends Animal {}
class SpecificDog extends Dog {}
```
Then you can use just `<?>` and that's is like saying that you can pass a list of any type. It's not like saying `List<Object>` because you can pass only a `List<Object>`as parameter of a method having that as argument. With `List<?>` you can pass any `List` you like but you cannot add anything because a `Dog` !IS-A a `Church` (you cannot add even a simple `Object`).

###Generics declarations
``` java SUPER EXAMPLE
// it's possible to declase several generics like <E,T>
// you can use extends and super but not ?, you'll get a compiler error
public interface List<E> {
	boolean add(E e);
	public E get(int i);
	// you can declare generics directly in a method. This interface compiles.	
	<T> T someMethod();
}
public interface Animal<E> {
	<E> void someMethod(E e);  
	// type shadowing!! This <E> is different from the one above
}

```
