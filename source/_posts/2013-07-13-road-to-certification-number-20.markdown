---
layout: post
title: "Road to Certification #20"
date: 2013-07-16 15:51
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Command line tools
**javac** is the command to control the compiler. The syntax is the following: `javac [options] [source files]`. Possible options are:

* `-d` is the option to say in which directory to put the .class files. If the java file has a **package** statement in it, then the tree of directoris will be recreated. It's possible to have a compiler error if the path passed to -d does not exists;
* `-source` is used to specify with which SDK you want to use

**java** is the command to invoke the JVM. The syntax is `java [options] class [args]`. You can specify only one class without the extension .class. It's possible to use the following options:

* `-Dprop=val` if the value contains space you have to use `-Dprop="my val"`. To get a value you can use `System.getProperty("prop");`
* - `[args]` it's a 0-indexed array and you can pass them to the main method:

``` java DECLARATION OF MAIN
public static void main(String[] args) {}
public static void main(String ... x) {}
public static void main(Strng args[]) {}
```

###Search for classes
**java** and **javac** search using the same alghorithm:

1. they look in the same list of directory and in the same order;
2. they stop as soon as they find the first occurrence of the class (others are ignored);
3. they first look in the SDK;
4. they secondo look in classpath;

A classpath can be defined using system variables or via command line with option `-classpath` or `-cp`. In the classpath they consider only the final directory of a path. Path separator is `:` and current directory is `.`. They search from left to right. (the current directory is used by javac by default, you have to specificy it for .class files)

###The import static
It's used to import static memebers of a class. It's possible also to import constants variables.
``` java IMPORT STATIC
import static java.lang.System.out; // member
import static java.lang.Integer.*; //every member of the class Integer
```
