---
layout: post
title: "Road to Certification #15"
date: 2013-07-11 19:27
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
## equals() and hasCode()
When you want to use an object as key of an hashtable, it's necessary to override `equals()` and `hashCode()`.

`public boolean equals(Object o)` has the following contract:

* `x.equals(x)` is always **true**;
* `x.equals(y)` <-> `y.equals(x)`;
* `x.equals(y)` and `y.equals(z)` -> `x.equals(z);
* `x.equals(y)` must return always the same value after every call;
* `x.equals(null)` is always **false**;
<!-- more -->
You can use the hashcode to shrink the research set, its signature is `public int hashCode()`. The contract:

* `hashCode` needs to return always the same value for an object during a single execution of an application;
* two `equals` objects must return the same `hashCode`;
* two not `equals` objects can return the same `hashCode`;

##Collections
You have two types of Collections:

* ordered: it's possible to iterate a collection in a specific order (for example the insertion order);
* sorted: the ordering is based on object properties (like the natural orders for numbers);

*`Map` does not implement `Collection`. `Set`, `List` and `Queue` implement `Collection`.*

###List interface
A class implementing a List is based on the usage of the index. It allows to have methods that use it like `get(int index)`, `add(int index, E element)` and `int indexOf(Object o)`. Lists are ordered using the index. When you are adding a new element, you are doing an append, unless you are going to specify and index.

`ArrayList` can be used to have easy access to the elements of the arrays via the index (you have *O(1)*). It's ordered, not sorted. You can use it when you don't do many adds or deletes. `ArrayList` grows dinamically. `Vector` is the thread-safe version of `ArrayList`.

`LinkedList` has elements linked between them. It's really easy to use it as a stack or a queue. It has methods to add at the end or at the beginning. It also implements `Queue`. It's not useful if you need to access it using the index.
