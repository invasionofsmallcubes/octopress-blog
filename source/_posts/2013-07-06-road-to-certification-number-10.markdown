---
layout: post
title: "Road to Certification #10"
date: 2013-07-06 20:26
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Control Flow Statement

* `if .. else if .. else`: both `else` and `else if` are indeed optional. If you have just one statement, you can avoid the usage of `{}`. You can use **boolean** or **Boolean** inside an `if`. If you are using the `else if` statements some rules are in place:

	1. it's possible to have zero or one `else` for every given if;
	2. you can have zero or more `else if` coming before an `else` (and `else` is optional, too);
	3. if an `else if` succeded, next `else if` and the final `else` will not be executed;

<!-- more -->
* `switch`: inside a switch you can have **char**, **byte**, **short**, **int** and **enum**, so everything you can cast to **int**. Inside `case` you have to put **compile-time constants**. You cannot use **float**, **double** and **long**. This is the syntax for a `switch`:
``` java SWITCH SYNTAX
		switch (variable) {
		case <compile-time constant>:

			break;

		default:
			break;
		}
```
`default` and `break` are optionals. It's not possible to have different `case`s with the same label. Remember that `'a'` equals to `97` so you cannot have both case in a switch, you'll get a compiler error. In the switch argument you can also have variables declared `final` and initialized so this is legal: `final int a = 0;`. Remember to assign the variable to a value or you'll get a compiler error. The `switch` statement base its checks on what you are passing. If you pass for example a **byte** a case with the value of 128 will be out of range and you'll get a compilation error. In a `switch` you can also use wrappers (unboxing FTW!) like **Byte**, **Integer** etc...

`case` are evaluated with an approch top-down and `default` can be anywhere inside a switch, even between `case`. When a `case` is matched, if there isn't a `break` statement, every remaining `case` will be executed sequentially until the end or until a `break` has been found.
``` java SWITCH SYNTAX
switch (3) {
		case 1:
			System.out.println(1);
		default:
			System.out.println('d');
		case 3:
			System.out.println(3); // printed
		case 2:
			System.out.println(2); // printed
		}
```

* `while` and `do...while`: the `while` loop takes a **boolean** expression. It's not possible to do declaration inside but it's possible to to do assignment inside:
``` java WHILE EXAMPLES
// unreachable codes
final boolean b = false;
while(b) {}
while(false) {}
// ok
boolean b = false;
while(b) {}
while(b=true){} // b assigned to true and then goes inside the while block
```
with the `do {..} while(expr);` loop the reasoing is the same but the instructuns are going to run at least once.
* Basic `for` loop: we have three parts in a `for` loop: the declaration ed inizialization of variables (having the scope of the `for`), the boolean expression and the iteration expression. The second part can have only one **boolean** expression. the third part has the iteration expression that can be anything (not only an increment). These are legal: `for(;;)` and `for (int i = 0, j = 0; i < 10; i = (i < 10) ? 10 : 1, j = 3) {}`. 

To go out of a loop you can use:

	1. **break** to exit from the current loop;
	2. **return** to exit from the method;
	3. `System.exit()` to exit from the program;

* Enhanced `for` loop: it can be used with arrays or collection (or classes implementing the `Iterable` interface). The syntax is `for(declaration:expression);` where the first part is the declaration of a variable of the type of an element of the array or the collection, the second part is the array or the collection.

* `break`: causes the loop to stop and goes to the first line after the loop;
* `continue`: causes the current iteration of the loop to end and starts with the next one inside the same loop after check that the boolean expression is still true;
* **labelled statement**: you declare a label like this `label:{}` and then you can use `break label;` to break the current execution and go to the label. You can use a label only inside the scope of the label;
