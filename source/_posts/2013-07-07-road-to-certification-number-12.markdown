---
layout: post
title: "Road to Certification #12"
date: 2013-07-08 12:13
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Strings
`String` is an immutable object. Every character of a string is Unicode 16-bit. The `String` class is marked **final**. To create a string I can do the following:
``` java STRING CREATION
String s = "hello";
String a = new String();
String c = new String("hello");
```
<!-- more -->
Please notice that `c == s` returns **false** because even if the *"hello"* string is the same one (there is just that one in the string pool), the object created is different. Remember that the String is indeed immutable, but not the variable that you can reassign the way you want.

If I have `s.concat("pippo")`, the variable `s` does not change its content, the method returns a new string *"hellopippo"*.

Some useful method to know:

* `public char charAt(int index)`: the index is 0-based, it returns the **char** at the index;
* `public String concat(String s)`: it's an append, really similar to the usage of `+` or `+=`;
* `public boolean equalsIgnoreCase(String s)`: verify equality of the content of two strings without case-sensitive check; 
* `public String substring(int index, int end)`: index is 0-based, end is 1-based since it's the offset (you can also think of it like end-1 if you want to think of 0-base index);
* `public String trim()`: returns the String without blank spaces at the end and at the beginning of the String;

###StringBuilder and StringBuffer
`StringBuilder` is like `StringBuffer` but it's not thread-safe because the methods are not `synchronized`. `StringBuilder` is available from Java 5. StringBuffer does not have the ovveride of equals, so it compares references. It has 3 constructors:

* `public StringBuilder append( (String|char|int|...) s)`: appends the new value and return itself;
* `public StringBuilder delete(int start, int end)`: deletes a chuck of the string and return itself (start is 0-base, end is 1-based);
* `public StringBuilder insert(int offset, (String|char|int|...) s)`: offset is 0-based, it inserts the content at that position and shift the rest;

##File navigation and I/0
A file is an object that represents in an abstract way a `File` or a `Directory` in the filesystem. It accepts as argument a path. If the file does not exists, the file will not be created.

To create it we use `createNewFile()` that returns false if the file exists already. If i try to create a file but the path hierarchy does not exists, we get an exception. There are other methods like `exists()`, `delete()`, `isDirectory()` and `mkdir()` and every one of them returns a **boolean**. One of the constructor of `File` can accept the path and another `File` so that you can build a file hierarchy.

A `FileWriter` accepts a `File` and allows to write a string in a file. Other methods are `flush()` and `close()`. A `FileReader` accepts a `File` and reads a certain number of chars with `read(char[] a)`. 

You can also find more abstract classes like `BufferedReader` or `BufferedWriter`. `BufferedWriter` has the method `newLine()` which `FileWriter` does not have. `BufferedReader` is able to use the method `readLine()` to read line by line until it returns **null** when there no more lines.

###Scanner and Tokenizing
With a Scanner you can find tokens. Here's some reason why is the best tool for the job:

* Scanners can be built from string files, streams and strings;
* tokenizing can be done with a loop and you can go out of the loop whenever you like;
* token can be automatically converted to primitives;

We have several methods to use with the string Scanner. You have `next()` and `hasNext()` to go through the loop but you also have `hasNextXxx` and `nextXxx` where `Xxx` is a primtive. With `useDelimiter` you can set a custom regular expression as delimiter. Also with the method `findInLine` that accepts also a regular expression, you can get the next occurrence of a pattern constructed from the specified string, ignoring delimiters.
