---
layout: post
title: "Road to Certification #16"
date: 2013-07-12 19:46
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Ordering Arrays And Collections
There are utility methods in classes `Arrays` and `Collections` to order elements.

The `sort` method accepts a collection of objects implementing the interface `Comparable`:

``` java COMPARABLE
public class MyClass implements Comparable<MyClass> {
	public int compareTo(MyClass myClass) {}
	// remember you have to declare the type as a generic
	// and you can use the real class as argument
	// in the signature
}
``` 

* if `this` < `myClass` then return a number **<= -1**;
* if `this` == `myClass` then return **0**; 
* if `this` > `myClass` then return a number **>= 1**;

The `sort` method has an overload that accepts a `Comparator` that gives us a way to order differently from the natural order.

``` java COMPARATOR
public class MyComparator implements Comparator<MyClass> {
	public int compare(MyClass a, MyClass b) {}
	// same RETURN RULES of Comparable
}
```

The class `Arrays` has the same overload of `Collections` plus a series of `sort` dedicate to primitive types that always order using the natural order. `sort`is **void** and does not return a new object but modify the one passed.

##Search Inside An Array or a Collection
Both utility classes use the method `binarySearch`:

* a research returns the integer indicating the position of an element (0-based index); 
* a research that doesn't find the element returns a negative integer which is the position of the element would be. The real position would be `-(insertion-position)-1`; 
* the collection/array must be ordered before doing the binary research;
* if it's not ordered the result will be not predictable;
* if the collection is ordered natural, you cannot use the search with a `Comparator`;
* if the collection is ordered with a `Comparator`, then you must use the `Comparator` in the binary search;

The signature is `static int binarySearch(array/collection, value to search [, Comparable])`.
