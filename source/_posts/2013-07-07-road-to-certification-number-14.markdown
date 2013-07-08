---
layout: post
title: "Road to Certification #14"
date: 2013-07-10 15:03
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Date, numbers and currency

* `java.util.Date`: a class with many deprecated method. Has a default constructor that returns a `Date` with the current time and date. It has another one accepting a **long** parameter corresponding to the milliseconds from Unix Time. You can use `void setTime(Date date)` and `Date getTime()` to set and get a date (there are also a getter and a setter accepting and returning a **long**);
<!-- more -->
* `java.util.Calendar`: abstract class. You have to use `getInstance()` method. You also have here a `(get|set)Time`. With `get` is possible to obtain a specific component of the date (e.g.: `Calendar.DAY_OF_THE_WEEK). With `add` we can add a specific unit of time to the date. With `roll` we add a unit of time like with `add` but without modifying the larger units of time; 
* `java.text.DateFormat`: this class is abstract. You have a `getInstance()` or `getDateInstance()`. The `format` method accepts a `Date` and returns a `String`. The method `parse` accepts a `String` and returns a `Date` expressed in the `Locale` passed in phase of creation. It can throw a `ParseException`;
* `java.util.Locale`: you have two constructors: `Locale(String language)` and `Locale(String language, String country)`. Locale must be passed in phase of construction of the `DateFormat`: `DateFormat.getInstance(DateFormat.FULL, new Locale("it"))`. It also has `getDisplayCountry()` and `getDisplayLanguage()` (they also can accept a Locale);
``` java LOCALE EXAMPLE
Locale l = new Locale("pt","BR"); // Portuguese from Brasil
l.getDisplayCountry() // it returns Brazil because the JVM has the US locale
l.getDisplayCountry(l); // Brasil, because we passed the Locale we created
```
* `java.text.NumberFormat`: abstract class. You can use `getInstance()` to format numbers or you can get `getCurrencyInstance()` for currencies. Both methods accept a `Locale`. As for the `DateFormat` class, you have here a `parse` and a `format` but in this case `format` accepts any type of number.

##Regexp
Remember that a quantifier of type greedy reads the entire string and then it gets the right-most match so if we have the regexp `.*xx` and the string is `yyxxxyxx` then the match is the entire string.

This is an example of regexp coding:
``` java REGEXP EXAMPLE
Pattern p = Pattern.compile("myregexp"); // first let's compile the regexp in a Pattern object
Matcher m = p.matcher("myregexpstring"); // let's create a Matcher for String we want to analyze
System.out.println(m.pattern()); // it prints the pattern "myregexp"
while (m.find()) { // for every occurrence found
	System.out.println(m.start() + " " + m.group()); // position and content of the occurrence
}
```

##Formatting
To do the job you can use `format` and `printf` from Java 5 for the class `PrintStream`.

Here's the syntax (`[]` means optional) : `%[arg_index$][flags][width][precision] conversion`.

* `arg_index` position in the var-arg you are passing to the method, 1-based;
* `flags`:
	* `-`: justify to the left;
	* `+`: add plus or minus sign;
	* `0`: pad with zero;
	* `,`: `Locale` specific separator;
	* `(`: negative numbers between parenthesis;
* `precision`: precision for floating-point;
* `conversion` : **b** boolean, **c** char, **d** integer, **f** floating-point, **s** string. It's possible to have `IllegalFormatConversionException` if we use `d` but then we pass a double;
