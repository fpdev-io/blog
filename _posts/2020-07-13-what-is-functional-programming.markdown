---
layout: post
title:  "What is Functional Programming?!"
date:   2020-08-01 13:01:16 +0100
categories: functional programming
author: fp_dev
---

Many developers want to learn Functional Programming these days but as it turns out it's not that easy.
It's easy when we try to explain someone what Functional Programming really is.  

We usually say: 
## `Functional Programming is a programming with functions.`
Some time ago I was Java Developer. One day I decided that I'd like to be Scala developer. I didn't have any previous experience with this language.

When I started learning it, it quickly turned out that it's not just a syntax to grab. It was the whole new world of programming with a very different approach to composing programs. It was Functional Programming.

In this blogpost I'm gonna explain Functional Programming by using **Scala**. I'll explain a bit what's going on in the
code and I'll try to use very simple examples.

Ok, having said that let's go back to the point.

# What is Functional Programming?

Functional Programming is a programming style by using functions:
{% highlight scala %}   
def func(): Unit = {
    println("hello World!")
}

{% endhighlight %}

This is a very simple function in Scala. It doesn't do much. It just prints "hello world" in the console.

As you can see we define functions in Scala by using **def** keyword. Every function in Scala must return a value. In
this case our function returns **Unit**.  

**Unit** in Scala is eviqvalent to **void** in Java.

Let's have a couple of functions:

{% highlight scala %}

def f(x: Int): Int = x + 1

def h(x: Int): Int = x + 2

def h(x: Int): Int = x + 10

{% endhighlight %}
