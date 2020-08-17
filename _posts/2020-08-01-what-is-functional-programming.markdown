---
layout: post
title:  "What is Functional Programming?!"
date:   2020-08-01 13:01:16 +0100
categories: functional programming
comments: true
author: fp_dev
---

Functional Programming is getting more and more popular nowadays.  

Many developers want to learn Functional Programming but as it turns out it's not that easy.
It's easy when we try to explain someone what Functional Programming really is.  
It gets harder when it comes to practice. There are lots of new words (monads, functors, applicatives, etc.). It's
completely new approach to programming software. Many developers struggle to understand it. 

Dozens of people say that functional programming is all about special syntax, lambda functions or special languages.
It's all true but these things above are only additions. Some even say that you can do FP only with Haskell or Erlang. 
Some time ago I was Java Developer. One day I decided that I'd like to be Scala developer. I didn't have any previous experience with this language.

When I started learning it, it quickly turned out that it's not just a syntax to grab. It was the whole new world of programming with a very different approach to composing programs. It was Functional Programming.

In this blogpost I'm gonna explain Functional Programming by using **Scala**. Why Scala? Because it's a very good hammer
for it. Scala allows writing OOP code as well as FP code. It helps when switching from OOP to FP languages. I'll explain a bit what's going on in the
code and I'll try to use very simple examples.

Ok, having said that let's go back to the point.

# What is Functional Programming?
It all comes down to saying that:
# `Functional Programming is a programming with functions and immutable data structures.`
A function relates every value of type **X** to exactly one value of type **Y**.

In Scala we could write:  
{% highlight scala %}
def f: X => Y
{% endhighlight %}


So, Functional Programming is a programming style by using functions:
{% highlight scala %}
def func(): Unit = {
    println("hello World!")
}

{% endhighlight %}

This is a very simple function in Scala. It doesn't do much. It just prints `hello world` to the console.

As you can see we define functions in Scala by using **def** keyword. Every function in Scala must return a value. In
this case our function returns **Unit**.  

**Unit** in Scala is eviqvalent to **void** in Java.

Let's have a couple of functions:

{% highlight scala %}

def f(x: Int): Int = x + 1

def g(x: Int): Int = x + 2

def h(x: Int): Int = x + 10

val x = 5

val a = f(x) /* we calculate a value of the first function */
val b = g(a) /* and we pass it to the next function then */
val c = h(b)

val d = h(g(f(x))) /* we compose functions together */
{% endhighlight %}

As you can see the code above looks just like simple equations in maths.

That's why we sometimes say that FP code is like algebra.

# Side Effects
Suppose we have a function: 
{% highlight scala %}
def increment(x: Int): Int = {
  println(s"x value: $x")
  x + 1
}
{% endhighlight%}

Everything is fine with that function...but it prints x value to the console.  
This action we call a `side effect.`

# Pure Functions

### `A pure function is a function where its output depends only on its input value.`  

So that a pure function:
* cannot read from I/O
* cannot write to I/O
* cannot modify any field outside of its scope

As pure functions don't communicate with I/O devices, then println's are forbidden.

As we could also say that pure functions don't have `side effects`.

{% highlight scala %}

var x = 5

/* Not a pure function. It changes x which is outside of the function's body */
def changeX(): Unit = {
  x = 10
}

{% endhighlight %}

Can we quickly recognise if function is not pure?  
Function's signature gives us some information. If function doesn't have input parameters or doesn't return anything.  

{% highlight scala %}
def impureFunc(): Unit = {
  ....
}
{% endhighlight %}

We see that this function doesn't depend on any input parameters and doesn't return any value.
We don't even have to know exactly what it does inside. Probably it just reads or writes data to I/O devices.

**There are lots of benefits when using pure functions:**
1. They are easy to reason about
2. They are composable
3. They are testable

# Referential Transparency
Referential Transparency is another technique for writing FP code.
### `An expression is referentially transparent if it can be replaced by its value.`

Or, when we know what pure functions are:

## `Rerefential Transparency provides a proof that our program works correctly by replacing pure functions with their values.`

It helps to debug and solve complext problems easily.

Here I'm giving you some exercises about RT. Please try to guess which one is referentially transparent and wchich is
not. The answers are at the end of the article.

**Exercise 1. Are these apps the same?**

{% highlight scala %}
  /* app 1 */
  val value = 13
  List(value, value)

  /* app 2 */
  List(13, 13)
{% endhighlight %}

**Exercise 2. Are these apps the same?**
{% highlight scala %}
  /* app 1 */
  val value = <expr>
  List(value, value)

  /* app 2 */
  List(<expr>, <expr>)
{% endhighlight %}

**Exercise 3. Are these apps the same?**
{% highlight scala %}
  /* app 1 */
  val value = iter.next()
  List(value, value)

  /* app 2 */
  List(iter.next(), iter.next())
{% endhighlight %}

**Exercise 4. Are these apps the same?**
{% highlight scala %}
  /* app 1 */
  val value = println("hello")
  List(value, value)

  /* app 2 */
  List(println("hello"), println("hello"))
{% endhighlight %}

# How it differs from OOP?
  
# Summary
In this short article I hope I explained Functional Programming a bit. I know it's just the tip of the iceberg and FP is
very extensive and exciting programming technique. In the next blogposts I'll give you more practical information about
FP bits and pieces like:
1. Monads, Functors, Applicatives
2. Immutable data
3. Data validation
4. Partial functions, partially applied functions and currying in Scala


<sup><sub>RT answers: yes, it depends*, no, no</sub></sup>  
<sup><sub>*it depends because if a given expression is constant then we have referential transparency otherwiese not</sub></sup>

