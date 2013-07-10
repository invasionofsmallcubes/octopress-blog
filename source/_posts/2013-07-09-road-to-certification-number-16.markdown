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
<!-- more -->
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

###Convertion of arrays to list and vice versa
`Arrays.asList` returns a list linked directly to the array is if I make a change, I'll see the change in both of them. You cannot add elements to a list generated in this way and you'll get an error.

`List` and `Set` have their method `toArray`. It has two overloads: one returning an array and another one that fills the array passed as argument.

####More on List usage
It's possible to iterate a list with the for each but in previous versions you could use an `Iterator` to do the same.
``` java ITERATOR EXAMPLE
List<MyClass> list = new LinkedList(); // doesn't matter the implementation you choose
Iterator<MyClass> i = list.iterator();
while(i.hasNext()) MyClass t = i.next(); //do something with "t"
}
```

##NavigableMap and NavigableSet
To find the first of the last element related to a specific key you can use these methods.

Lowest element bigger than `e`/`key`:

* `TreeSet.ceiling(e)` (ceiling is >=);
* `TreeMap.ceilingKey(key)` (ceiling is >=);
* `TreeSet.higher(e)` (higher is >);
* `TreeMap.higherKey(key)` (higher is >);

The highest element smaller than `e`/`key`:

* `TreeSet.floor(e)` (floor is <=);
* `TreeMap.floorKey(key)` (floor is <=);
* `TreeSet.lower(e)` (lower is <);
* `TreeMap.lowerKey(key)` (lower is <);

Taking the first or the last element:

* `TreeSet.pollFirst()`;
* `TreeMap.pollFirstEntry()`;
* `TreeSet.pollLast()`;
* `TreeMap.pollLastEntry()`;

Reverse order:

* `TreeSet.descendingSet()`;
* `TreeMap.descendingMap()`;

##Backed Collections
There are two methods to return subcollections. These subcollection are linked, so if I add an element to one of the collection, the other one will see that element added. The subcollection has a range, so if you add an element outside that range, you'll get a runtime exception.

Subset or submap from the head until `e`/`key` excluded (b is **false** by default):
* `headSet(e, b*)`;
* `headMap(key, b*)`;

Subset or submap starting from `e`/`key` include to the end:
* `tailSet(e, b*)`;
* `headMap(key,b*)`;

Subset or submap from s (included) to e (excluded):
* `subSet(s, b*, e, b*);
* `subMap(s, b*, e, b*);
