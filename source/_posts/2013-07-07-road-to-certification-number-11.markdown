---
layout: post
title: "Road to Certification #11"
date: 2013-07-07 11:11
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Exception Handling
The syntax for handling exception is:
``` java EXCEPTION HANDLING
try {}
catch (<MyException> e) {}
finally {}
```
If there is a try you need a `catch` or a `finally` or both. Every `catch` must precede the `finally` and they must be declared respecting the hierarchy from the more specialized to the less specialized (e.g. `FileNotFoundException` before `IOException`).
<!-- more -->
The code inside the `finally` is always executed, even if there is a `return` inside the `try`.

It's possible to throw exceptions with the statement `throw`. You can throw every class descending from `Throwable`.

We have two type of exception: **checked** and **unchecked** exception. If an exception is **checked** this means that you have to handle it through a `try...catch` or you need to add to the method signature the clause `throws`, like `public void readFromFile() throws IOException {}`.

`Error` and `Exception` extend `Throwable`, `RuntimeException` extends `Exception`. `Error`, `Throwable` and `RuntimeException` are **unchecked**, `Exception` is checked.

##Assertions
You can use it to identify the *truth* about some statements when you are **not** in production. We have two types of assertions:

* `assert(<boolean expression>)`;
* `assert(<boolean expression>): <statement returning a value>`;

The second one gives you some more information and converts the second statement in a string. If the boolean expression is false then we'll have an **AssertionError** and you MUST NOT HANDLE IT, remember, it's not in production!

> ####Be aware that:
> before Java 1.4 **assert** could be used as an identifier, so if we have a source code written before 1.4, we need to specify `javac -source 1.3 com/Class.java` so that **assert** will not be used as language keyword.

> The option *-source* accept 1.3, 1.4, 1.5, 5, 1.6, 6

To enable or disable assertion at runtime:

* `java -ea` or `java -enableassertions` to enable them;
* `java -da` or `java -disableassertions` to disable them;
* `java -ea: com.foo.Bar` to enable them for a specific class;
* `java -ea: com.foo...` to enable them for a specific package and all subpackages;
* `java -ea -dsa` enable all the assertions except the ones from system classes;
* `java -ea -da:com.foo...` enable all the assertions except for a specific package;

###How to use assertions
An `AssertionError` should not be handled.

An assertion must not be used when:

* I want to validate arguments of a public method because when you disable them you are also disabling the validation;
* I want to validate command-line arguments;
* I risk to have side effects. Like when you are doing `assert(booleanMethod())` it's true that you are getting a boolean but are you sure that inside the method the state of the object is not changing?

An assertion can be used when:

* I want to validate arguments of a private method because if it's private you can assume the logic is correct (you already validated input coming from a public method using this private method);
* I want to assert cases that, even in production, will never happen;
