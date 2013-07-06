---
layout: post
title: "Road to Certification #9"
date: 2013-07-05 18:01
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Comparison Operators

* **compound assignment operator**: +=, -=, *=, and /=. The right expression gets evaluated first, so for example: `x *= 2 + 5` is equals to `x = x * (2+5)`;
* **relational operators**: <, <=, >, >=, ==, !=. The result of this operator is a **boolean**. It's legal to use them to compare *ints*, *floating-points* and *chars*. Also, it should be already clear, but you can compare a **char** to an **int** because the JVM uses the unicode value of the character;
<!-- more -->
* **equality operators**: ==, !=. It's possible to use them to compare numbers, boolean, char and object references. It's not possible to compare between them not compatible types like **char** and **boolean**. With primitive types, equality tests the value of them, whereas with objects it tests if the to reference are pointing to the same object in the heap;
* **instanceof** can be used only for objects. It is a test on the IS-A relationship. It's bidirectional mean that I can test if a class is a *superclass* of its subclass. You can also use it for interfaces. `a instanceof null` always returns **false**. You'll get a compilation error if the variable type used is not in the inheritance hierarchy;
* **String concatenation operator*: +. You can use it to concatenate strings. It's possible to use concatenation between Strings and other types (it will be used the `toString()` method in case of objects). You can also use += to concatenate with the same rules explained early;
* **Conditional operator (ternary operator)**: `x = (boolean expression) ? <value if true> : <value if false>. It's possible to nest them;
* **Logical operator**: `&`, `|` and `^` (XOR - true only if 1 0 or 0 1) are not short-circuit so the valutation is not partial. Remember it, you'll get plenty of exercise confusing between the usage of those.

> ####Be aware that:
> `b=false; if(b=true);` it's legal because you are first assigning *b* to **true** and then it gets evaluated. For string concatenation be aware of the following usage:
{% codeblock lang:java %} 
byte u = 3; 
System.out.println( u+1 ); // 4 
System.out.println( u+1+"text");  // 4text
System.out.println((u+1)+"text"); // 4text
System.out.println("text"+u+1); // text31
System.out.println("text"+(u+1)); // text4
{% endcodeblock %}

