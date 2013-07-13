---
layout: post
title: "Road to Certification #19"
date: 2013-07-15 15:50
comments: true
categories: [Sun, Certification, SCJP, OSCJP, JAVA6]
---
##Java Concurrency
With the word *thread* in Java we indicates two things:

* an instance of a `java.lang.Thread`, so basically an object living in memory heap;
* a *thread of execution*, a process with its own stack in memory. In Java one thread has one callstack;

There two types of thread: a user and a demon thread. JVM exits from executon only when every user thread has finished. It doesn't consider demon threads status.

You can create a Thread *extending* the class `Thread` or implementing the interface `Runnable`. The method to override in both cases is `public void run()`. It's legal to overload `run()` but only `public void run()` is considered when it comes to create a new thread of execution.

To instantiate a thread we have four constructors: 

* `Thread()`;
* `Thread(Runnable target)`;
* `Thread(Runnable target, String name)`;
* `Thread(String name)`;

It's possible to pass the same instance of `Runnable` to several thread without problem (well, beware of shared data!). When a `Thread` has been create it is in the state **new**, when you call `start()`, the state is **runnable** and a new thread of excution is created but the execution doesn't start. The thread scheduler decides when a thread has to start the excution, you cannot control it (you can use priorities though).

> ####Be aware that:
> It's legal to call directly the method `run()` as long as it's clear that you are not creating a new thread of excution. That's possible only when you call `start()`.

To set a name of a Thread you can use `setName()`. If you are using a `Runnable`, you can access the name from `Thread.currentThread.getName(), if you have no way to access to the instance of the thread. The name of the thread associated to the method `main`, is "main" (duh!).

When you excute more then one thread, you can assure that every thread will be executed, but you can't say anything about the order of execution of each thread. When the thread has finished the execution of `run()`, the thread will be in the state **dead**.

###States of a Thread

* **NEW**: instance of Thread created(), `start()` has not been called yet;
* **RUNNABLE**: `start()` has been called and we have a thread of execution, the thread is not running yet;
* **RUNNING**: `run()` has been executed;
* **WAITING**/**BLOCKED**/**SLEEPING**: the thread is alive but it's not possible to run it, like because is blocked for an I/O operation;
* **DEAD**: the method run has finished;

###Thread methods

* `sleep()` it's static and accepts the number of milliseconds. It does not release acquired locks. Launches a `InterruptedException`; 
* `yield()` it's static and launches an `InterruptedException`. It tells to the current thread to go back to the state runnable to leave space to other threads but remember that the scheduler decides what to do;
* `join()` it's an instance method, when called tells to the current thread to wait for the thread who called the `join()` to end. It launches an `InterruptedException`;

###Thread priority

In many cases the thread in state **running** will be the one that has higher priority or equal to the thread with the higher priority in **runnable** state.

A thread has initially the same priority of the current thread where it gets instantiated, but you can set it directly with `setPriority()`.

In Java the default priority is 5. You also have `Thread.MIN_PRIORITY`, `Thread.NORM_PRIORITY`, `Thread.MAX_PRIORITY`. It's JVM implementation dependent.

###Synchronizing

* it's possible to syncronize only methods or code blocks;
* every object and every class have an intrinsic lock;
* a class can have both synchronized and not syncronized methods;
* `sleep` does not release locks;
* if a thread has already acquired a lock, you use other syncronized methods using that lock;

###Method of the Object class
`wait()`, `notify()` and `notifyAll()` are instance methods of the class `Object` and they are called only in a syncronized context otherwise you'll get a runtime exception.  `wait()` releases acquired locks.
